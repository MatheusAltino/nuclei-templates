# Custom Nuclei Templates

Repositório de templates customizados para o Nuclei, focado em exposições, misconfigurations, CVEs recentes e detecções úteis para threat intelligence e reconhecimento ofensivo/defensivo.

## Estrutura

```
http/
├── cves/2026/           # Templates de CVEs (organizados por ano)
├── exposures/          # Arquivos sensíveis expostos (.git, .env, etc)
└── misconfiguration/   # Configurações inseguras
workflows/              # Workflows de templates
```

## Uso

```bash
# Scan com todos os templates locais
nuclei -t http/ -u https://target.com

# Apenas exposures
nuclei -t http/exposures/ -u https://target.com

# Apenas CVEs
nuclei -t http/cves/ -u https://target.com

# Com tags
nuclei -tags cve,exposure,git -u https://target.com

# Lista de alvos
nuclei -t http/ -l targets.txt
```

## Templates incluídos

### Exposures / Misconfiguration
- `http/exposures/exposed-git-config.yaml` — Detecta `.git/config` exposto
- `http/exposures/exposed-env-file.yaml` — Detecta arquivos `.env` expostos
- `http/misconfiguration/directory-listing.yaml` — Detecta directory listing

### CVEs (2026)
Templates de CVEs recentes em `http/cves/2026/`. Classificação de qualidade:
- **FULL_VALIDATION**: CVE-2026-133968, CVE-2026-126752, CVE-2026-126755
- **PARTIAL_POC**: CVE-2026-59310
- **VERSION_FINGERPRINT**: CVE-2026-0322, CVE-2026-118207, CVE-2026-126259, CVE-2026-76466
- **EXPOSURE_ONLY / weak**: CVE-2026-126253 (recomendado reescrever)

## Adicionar novos templates

1. Crie o arquivo YAML no diretório apropriado (`http/cves/YYYY/` para CVEs)
2. Siga o padrão de `id`, `info` e matchers específicos
3. Prefira validação real (PoC) sobre fingerprint puro quando possível
4. Teste localmente: `nuclei -t seu-template.yaml -u https://testphp.vulnweb.com`

## Referências

- [Documentação oficial Nuclei](https://docs.projectdiscovery.io/templates/introduction)
- [Template Creation Guide](https://github.com/projectdiscovery/nuclei-templates/blob/main/TEMPLATE-CREATION-GUIDE.md)
