# Evidencia SBOM - OVERFORE TI-11

Evidencia de la seccion 3.6 del trabajo de investigacion ICI-5444.

Proyecto analizado: road-to-fire, commit 5509b73.
SBOM en formato CycloneDX 1.7, generados el 19 de septiembre de 2026.
Analisis con Grype 0.119.0, base de vulnerabilidades v6.1.9 del 19-09-2026.

## Contenido

- `sbom/syft.cdx.json` - Syft 1.52.0, configuracion por defecto. 42 componentes de terceros.
- `sbom/syft-dev.cdx.json` - Syft 1.52.0 con dependencias de desarrollo. 1158 componentes de terceros.
- `sbom/cdxgen.cdx.json` - cdxgen 12.8.4. 1158 componentes de terceros.
- `vulnerabilidades/grype-syft.json` - 24 coincidencias.
- `vulnerabilidades/grype-syft-dev.json` - 121 coincidencias.
- `vulnerabilidades/grype-cdxgen.json` - 121 coincidencias.
- `log-comandos.txt` - registro de la sesion de consola.

Los conteos son de componentes de terceros. No se cuenta el paquete raiz del
proyecto ni el archivo de bloqueo, que los generadores registran aparte.

## Comandos

```
git clone https://github.com/GabrielSanzana/road-to-fire.git
git checkout 5509b73
cdxgen -t javascript --spec-version 1.7 -o cdxgen.cdx.json .
docker run --rm -v "%cd%":/app anchore/syft:v1.52.0 dir:/app -o cyclonedx-json@1.7=/app/syft.cdx.json
docker run --rm -e SYFT_JAVASCRIPT_INCLUDE_DEV_DEPENDENCIES=true -v "%cd%":/app anchore/syft:v1.52.0 dir:/app -o cyclonedx-json@1.7=/app/syft-dev.cdx.json
docker run --rm -v "%cd%":/app anchore/grype:v0.119.0 sbom:/app/cdxgen.cdx.json -o json > grype-cdxgen.json
docker run --rm -v "%cd%":/app anchore/grype:v0.119.0 sbom:/app/syft.cdx.json -o json > grype-syft.json
docker run --rm -v "%cd%":/app anchore/grype:v0.119.0 sbom:/app/syft-dev.cdx.json -o json > grype-syft-dev.json
```
