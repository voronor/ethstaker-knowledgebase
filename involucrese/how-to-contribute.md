# Como contribuir

Este es un sitio de documentación vivo, lo que significa que necesitamos la ayuda de la comunidad para mantener y actualizar el contenido. Cualquier contribución, desde escribir secciones completas y traducciones hasta corregir errores ortográficos y gramaticales, será muy apreciada.

&#x20;Puedes ganar GitPOAP contribuyendo directamente a la Base de conocimiento de EthStaker ([Un contribuyente](https://www.gitpoap.io/gp/881)) y haciendo una pregunta que conduzca a la creación de contenido ([un colaborador↗](https://www.gitpoap.io/gp/923))..

[![EthStaker Knowledge Base Contributor GitPOAP 2023](https://www.gitpoap.io/\_next/image?url=https%3A%2F%2Fassets.poap.xyz%2Fgitpoap3a-2023-ethstaker-knowledge-base-contributor-2022-logo-1671596764627.png\&w=384\&q=75)](https://www.gitpoap.io/gp/881)[![EthStaker Knowledge Base Supporter GitPOAP 2023](https://www.gitpoap.io/\_next/image?url=https%3A%2F%2Fassets.poap.xyz%2F2023-ethstaker-knowledge-base-supporter-2022-logo-1672411990803.png\&w=384\&q=75)](https://www.gitpoap.io/gp/923)

Para sugerir cambios o agregar contenido nuevo, visite nuestro [EthStaker Github↗](https://github.com/eth-educators/ethstaker-knowledgebase) o si tiene alguna pregunta, únase a nuestro [Discord↗](https://www.google.com/url?sa=t\&rct=j\&q=\&esrc=s\&source=web\&cd=\&cad=rja\&uact=8\&ved=2ahUKEwjpm6nC5K78AhUBi1wKHaxHCF8QFnoECAsQAQ\&url=https%3A%2F%2Fdiscord.com%2Finvite%2FucsTcA2wTq\&usg=AOvVaw0U61EK\_8NaT71SEZlw3aJS)

Cree una solicitud para cualquier cambio que desee realizar y lo revisaremos lo antes posible.

* [Documentacion, estandariacion de notas](how-to-contribute.md#documentacion-estandarizacion-de-notas)
* [Crear/Actualizar tablas de contenido](how-to-contribute.md#crear-actualizar-tablas-de-contenido)
* [Glosario y pedido de encabezados de preguntas frecuentes](how-to-contribute.md#glosario-y-pedido-de-encabezados-de-preguntas-frecuentes)
* [Soporte Futuro para multi-lenguaje](how-to-contribute.md#future-support-for-multi-language)

## Documentacion, estandarizacion de  notas

Utilice estas notas cuando escriba para esta base de conocimientos para mantener un formato estandarizado.

* Use [enlaces relativos↗](https://github.blog/2013-01-31-relative-links-in-markup-files/) para navegar entre diferentes archivos dentro de esta base de conocimiento.
* `[Other file link](other_file.md)` → [Other file link](how-to-contribute.md)
* Use enlaces de anclaje a encabezados dentro del mismo archivo.
  * `[Anchor link](#heading-anchor)` → [Anchor link](how-to-contribute.md#documentacion-estandarizacion-de-notas)
* Combine enlaces relativos a otros archivos con enlaces ancla.
  * `[Other file anchor link](other_file.md#heading-anchor)` → [Other file link](how-to-contribute.md#documentation-standardization-notes)
* Mostrar cuando un enlace hace referencia a un sitio externo agregando el  ↗ icono al final del enlace.
  * `[External site link ↗](https://example.com)` → [External site link ↗](https://example.com)
* Crea una imagen que también sea un enlace.
  * `[![image-text](https://some.site/your-image.jpg)](https://some.site/your-link.html)`

## Crear/Actualizar tablas de contenido

Las tablas de contenido se crean usando una extensión de VSCode [Markdown All in One ↗](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) usando el comando `Create Table of Contents` (en el [VS Code Command Palette ↗](https://code.visualstudio.com/docs/getstarted/userinterface#\_command-palette)) para insertar una nueva tabla de contenido. Luego debería actualizarse automáticamente cuando se guarda un archivo.

Agrega la etiqueta `<!-- omit in toc -->` a cualquier encabezado que no desee que se incluya en la Tabla de contenido.

```
# HEADING <!-- omit in toc -->
```

## Glosario y pedido de encabezados de preguntas frecuentes

Al agregar elementos al Glosario y Preguntas frecuentes, es importante que permanezcan en orden alfabético para que sea más fácil navegar. Como no existe una forma nativa de lograr esto en Markdown, puede usar este script bash para reordenar los encabezados.

> El nombre del archivo `alphabetical-ordering.sh` se ha agregado al archivo .gitignore.

```
touch alphabetical-ordering.sh
chmod 700 alphabetical-ordering.sh
```

Edite el nuevo archivo con su editor de texto preferido.

```
#!/bin/bash
# Reorder glossary and store just the reordered content in a temp file
perl -0777 -ne '
    (undef,@paragraphs) = split /^##(?=[^##])/m;
    print map {"##$_"} sort @paragraphs;
' staking-glossary.md > staking-glossary-temp-1.md

# Delete everything after the first --- in and store in a temp file
sed '/---/q' staking-glossary.md > staking-glossary-temp-2.md

# Combine the two files
cat staking-glossary-temp-2.md > staking-glossary.md
cat staking-glossary-temp-1.md >> staking-glossary.md

# Delete the temp files
rm staking-glossary-temp-1.md
rm staking-glossary-temp-2.md


# Reorder FAQ and store just the reordered content in a temp file
perl -0777 -ne '
    (undef,@paragraphs) = split /^##(?=[^##])/m;
    print map {"##$_"} sort @paragraphs;
' faq.md > faq-temp-1.md

# Delete everything after the first --- and store in a temp file
sed '/---/q' faq.md > faq-temp-2.md

# Combine the two files
cat faq-temp-2.md > faq.md
cat faq-temp-1.md >> faq.md

# Delete the temp files
rm faq-temp-1.md
rm faq-temp-2.md
```

Ejecute el script.

```
./alphabetical-ordering.sh
```

> Esta fue una secuencia de comandos rápida, así que si tiene alguna mejora, ¡actualícela aquí!