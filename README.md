
name: 🎨 Deploy All to Render

on:
  push:
    branches: [main]

jobs:

  # ============================
  # 🔐 نشر المنصة الرئيسية
  # ============================
  deploy-main:
    name: 🔐 Deploy Main Platform
    runs-on: ubuntu-latest
    if: |
      contains(github.event.head_commit.modified, 'jwt-auth-app/')
    steps:
      - name: 🚀 Trigger Render Deploy
        run: |
          curl -X POST \
            "https://api.render.com/v1/services/${{ secrets.RENDER_MAIN_SERVICE_ID }}/deploys" \
            -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" \
            -H "Content-Type: application/json" \
            -d '{}'

      - name: ✅ Confirm Deploy
        run: echo "✅ Main Platform deployment triggered!"

  # ============================
  # 📢 نشر موقع الإعلانات
  # ============================
  deploy-ads:
    name: 📢 Deploy Ads Website
    runs-on: ubuntu-latest
    if: |
      contains(github.event.head_commit.modified, 'aghati-ads-website/')
    steps:
      - name: 🚀 Trigger Render Deploy
        run: |
          curl -X POST \
            "https://api.render.com/v1/services/${{ secrets.RENDER_ADS_SERVICE_ID }}/deploys" \
            -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" \
            -H "Content-Type: application/json" \
            -d '{}'

      - name: ✅ Confirm Deploy
        run: echo "✅ Ads Website deployment triggered!"

  # ============================
  # 👑 نشر الموقع الإمبراطوري
  # ============================
  deploy-imperial:
    name: 👑 Deploy Imperial Website
    runs-on: ubuntu-latest
    if: |
      contains(github.event.head_commit.modified, 'aghati-imperial-website/')
    steps:
      - name: 🚀 Trigger Render Deploy
        run: |
          curl -X POST \
            "https://api.render.com/v1/services/${{ secrets.RENDER_IMPERIAL_SERVICE_ID }}/deploys" \
            -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" \
            -H "Content-Type: application/json" \
            -d '{}'

      - name: ✅ Confirm Deploy
        run: echo "✅ Imperial Website deployment triggered!"

  # ============================
  # 🎯 نشر موقع Skill
  # ============================
  deploy-skill:
    name: 🎯 Deploy Skill Website
    runs-on: ubuntu-latest
    if: |
      contains(github.event.head_commit.modified, 'aghati-skill-website/')
    steps:
      - name: 🚀 Trigger Render Deploy
        run: |
          curl -X POST \
            "https://api.render.com/v1/services/${{ secrets.RENDER_SKILL_SERVICE_ID }}/deploys" \
            -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" \
            -H "Content-Type: application/json" \
            -d '{}'

      - name: ✅ Confirm Deploy
        run: echo "✅ Skill Website deployment triggered!"

  # ============================
  # 📊 تقرير النشر
  # ============================
  notify:
    name: 📊 Deploy Report
    runs-on: ubuntu-latest
    needs: [deploy-main, deploy-ads, deploy-imperial, deploy-skill]
    if: always()
    steps:
      - name: 📊 Report
        run: |
          echo "================================"
          echo "🎨 ALAAGHA Deploy Report"
          echo "================================"
          echo "🔐 Main:     ${{ needs.deploy-main.result }}"
          echo "📢 Ads:      ${{ needs.deploy-ads.result }}"
          echo "👑 Imperial: ${{ needs.deploy-imperial.result }}"
          echo "🎯 Skill:    ${{ needs.deploy-skill.result }}"
          echo "================================"
