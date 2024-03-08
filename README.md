# Listado de clasificaciones del catálogo de productos y servicios del SAT

[![Source Code][badge-source]][source]
[![Discord][badge-discord]][discord]
[![Latest Version][badge-release]][release]
[![Build Status][badge-build]][build]

Este repositorio contiene el **Listado de clasificaciones del catálogo de productos y servicios del SAT** que el [Servicio de Administración Tributaria (SAT)](http://www.sat.gob.mx/) expone en la aplicación web llamada [Catálogo de productos y servicios](http://pys.sat.gob.mx/PyS/catPyS.aspx).

El *Catálogo de productos y servicios* se expone dentro de un archivo de Excel. Sin embargo, el listado de clasificaciones no es expuesto en ningún lugar. Por ello es que esta información es recopilada y publicada en este repositorio.

Los 4 niveles de clasificación son: Tipo, Segmento, Familia y Clase.

- Tipo: Productos o servicios.
- Segmento: 2 dígitos usados como prefijo, no incluye el tipo como un prefijo.
- Familia: 4 dígitos usados como prefijo, incluye el prefijo del segmento.
- Clase: 6 dígitos usados como prefijo, include el prefijo de la familia.

Los 6 dígitos de la clase incluye los 4 dígitos de la familia, los 4 dígitos incluyen los 2 dígitos del segmento.

En el *Catálogo de productos y servicios* se expone un producto con la nomenclatura `SSFFCCXX` donde `SS` son los 2 dígitos del segmento, `SSFF` son los 4 dígitos de la familia, `SSFFCC` son los 6 dígitos de la clase y `XX` es un número *regularmente* consecutivo.

Por ejemplo:

- Clave de producto y servicio: "10121802 - Comida húmeda para perros"
- Segmento: "10 - Material Vivo Vegetal y Animal, Accesorios y Suministros".
- Familia: "1012 - Comida de animales".
- Clase: "101218 - Alimento para perros y gatos".

## Uso del recurso

El recurso es publicado en dos formatos:

- XML: <https://github.com/phpcfdi/resources-sat-pys/blob/main/data/pys.xml>.
- JSON: <https://github.com/phpcfdi/resources-sat-pys/blob/main/data/pys.json>.

### Formato XML

Para el formato XML se sigue la siguiente estructura:

```xml
<pys>
    <type key="1" name="Productos">
        <segment key="10" name="Material Vivo Vegetal y Animal, Accesorios y Suministros">
            <family key="1012" name="Comida de animales">
                <class key="101218" name="Alimento para perros y gatos"/>
                <!-- más nodos class -->
            </family>
            <!-- más nodos family -->
        </segment>
        <!-- más nodos segment -->
    </type>
    <!-- más nodos type -->
</pys>
```

### Formato JSON

Para el formato JSON se sigue una estructura de arreglo de objetos, donde cada objeto tiene una llave `key`, un nombre `name` y ningún o un hijo dependiendo del nivel en la estructura: Un *tipo* contiene `segments`, un *segmento* contiene `families`, una *familia* contiene `classes` y una *clase* no contiene hijos.

```json5
[
    {
        "key": 1,
        "name": "Productos",
        "segments": [
            {
                "key": 10,
                "name": "Material Vivo Vegetal y Animal, Accesorios y Suministros",
                "families": [
                    {
                        "key": 1012,
                        "name": "Comida de animales",
                        "classes": [
                            {
                                "key": 101218,
                                "name": "Alimento para perros y gatos"
                            },
                            // más objetos que representan una clase
                        ]
                    },
                    // más objetos que representan una familia
                ]
            },
            // más objetos que representan un segmento
        ]
    },
    // más objetos que representan un tipo
]
```

### Por qué XML y JSON en lugar de XML

A diferencia de la información de los Catálogos del SAT, el **Listado de clasificaciones del catálogo de productos y servicios del SAT** contiene una estructura muy poco cambiante y gerárquica, que se representa mejor en estos formatos.

## Actualización del recurso

Las actualizaciones al repositorio pueden ser consultadas en el archivo [`CHANGELOG`](./CHANGELOG.md).

El proceso de actualización es automático y se genera gracias al programa [`phpcfdi/sat-pys-scraper`](https://github.com/phpcfdi/sat-pys-scraper) para poder generar la información y exportarla con formato XML o JSON.

En caso de encontrar que el repositorio no está actualizado, por favor genera un `Issue` en este repositorio, explicando qué archivo falta o sobra o contiene datos no actualizados.

## Versiones del proyecto

Este proyecto tiene el siguiente versionado: `Estructura.Datos.Fecha`, por ejemplo `1.5.20191216`.

- `Estructura`: Hay un cambio en la versión mayor si el formato ha cambiado en su estructura.
- `Datos`: Hay un cambio en la versión menor si han cambiado los datos pero no la estructura.
- `Fecha`: Hay un cambio siempre que se crea una nueva versión.

El número de versión actual está almacenado en el archivo `data/version.txt`.

## Acerca de este proyecto

Este recurso se crea dentro de la iniciativa de [PhpCfdi](https://www.phpcfdi.com) para contar con información pública del SAT pero de forma descentralizada, con control de cambios y utilizable en formatos abiertos para sistemas informáticos.

Estos recursos, a pesar de estar vinculados con una tecnología en su formato, no están vinculados con un lenguaje de programación o una librería específica para su consumo. Cualquier proyecto, privado o público, desde cualquier lenguaje de programación, arquitectura o tecnología debe ser capaz de explotarlo siempre que pueda utilizar el formato de almacenamiento.

## Licencia

La información dentro de este repositorio debe ser considerada de *dominio público*, dado que es una recopilación de información pública generada por el [Servicio de Administración Tributaria (SAT)](https://www.sat.gob.mx/) de México. Debido a lo anterior, se establece este repositorio con la licencia [Unlicense](LICENSE).

[source]: https://github.com/phpcfdi/resources-sat-pys
[discord]: https://discord.gg/aFGYXvX
[release]: https://github.com/phpcfdi/resources-sat-pys/releases
[build]: https://www.phpcfdi.com/resources-app/build/sat-pys

[badge-source]: https://img.shields.io/badge/source-phpcfdi/resources--sat--pys-blue?logo=github
[badge-discord]: https://img.shields.io/discord/459860554090283019?logo=discord
[badge-release]: https://img.shields.io/github/v/tag/phpcfdi/resources-sat-pys?label=version&logo=git
[badge-build]: https://img.shields.io/endpoint?url=https%3A%2F%2Fwww.phpcfdi.com%2Fresources-app%2Fapi%2Fv1%2Fbuilds%2Fsat-pys%2Fshields.io&logo=github-actions
