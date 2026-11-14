# Custom Nuclei Templates

Repositório de templates customizados para o Nuclei, focado em exposições, misconfigurations e detecções úteis para threat intelligence e reconhecimento ofensivo/defensivo.

## Estrutura

```
http/
├── exposures/          # Arquivos sensíveis expostos (.git, .env, backups, etc)
├── misconfiguration/   # Configurações inseguras
└── vulnerabilities/    # Vulnerabilidades específicas
workflows/              # Workflows de templates
```

## Uso

```bash
# Scan com templates locais
nuclei -t http/ -u https://target.com

# Apenas exposures
nuclei -t http/exposures/ -u https://target.com

# Com tags
nuclei -tags exposure,git -u https://target.com

# Lista de alvos
nuclei -t http/ -l targets.txt
```

## Templates incluídos

- `http/exposures/exposed-git-config.yaml` — Detecta `.git/config` exposto
- `http/exposures/exposed-env-file.yaml` — Detecta arquivos `.env` expostos
- `http/misconfiguration/directory-listing.yaml` — Detecta directory listing

## Adicionar novos templates

1. Crie o arquivo YAML no diretório apropriado
2. Siga o padrão de `id`, `info` e matchers específicos
3. Teste localmente: `nuclei -t seu-template.yaml -u https://testphp.vulnweb.com`

## Referências

- [Documentação oficial Nuclei](https://docs.projectdiscovery.io/templates/introduction)
- [Template Creation Guide](https://github.com/projectdiscovery/nuclei-templates/blob/main/TEMPLATE-CREATION-GUIDE.md)
