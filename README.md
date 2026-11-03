name: 📊 GitHub Metrics

on:
  schedule:
    - cron: "0 3 * * *"   # todo dia às 00:00 (horário de Brasília)
  workflow_dispatch:      # permite rodar manualmente

permissions:
  contents: write

jobs:
  metrics:
    runs-on: ubuntu-latest
    steps:
      # Card geral: commits, PRs, issues, repositórios, estrelas...
      - name: 📊 Estatísticas gerais
        uses: lowlighter/metrics@latest
        with:
          filename: metrics.base.svg
          token: ${{ secrets.METRICS_TOKEN }}
          committer_token: ${{ secrets.GITHUB_TOKEN }}
          user: LucasBlackS2
          template: classic
          base: header, activity, community, repositories
          config_timezone: America/Sao_Paulo
          # conta também os repositórios de outras pessoas em que você colabora
          repositories_affiliations: owner, collaborator, organization_member

      # Card de linguagens, incluindo repositórios em que você colabora
      - name: 🧬 Linguagens
        uses: lowlighter/metrics@latest
        with:
          filename: metrics.plugin.languages.svg
          token: ${{ secrets.METRICS_TOKEN }}
          committer_token: ${{ secrets.GITHUB_TOKEN }}
          user: LucasBlackS2
          base: ""
          config_timezone: America/Sao_Paulo
          repositories_affiliations: owner, collaborator, organization_member
          plugin_languages: yes
          plugin_languages_limit: 8
          plugin_languages_details: percentage
          plugin_languages_ignored: html, css, dockerfile, shell
