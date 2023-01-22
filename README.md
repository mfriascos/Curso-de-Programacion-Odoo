# Odoo_New

<h2>Content List</h2>

- [Qué se Debe Saber del DESARROLLO Odoo](#qué-se-debe-saber-del-desarollo-odoo)
- [Arquitectura y Estructura básica de una app en Odoo](#arquitectura-y-estructura-básica-de-una-app-en-odoo)
- [Módelos Python para Aplicaciones Odoo](#módelos-python-para-aplicaciones-odoo)
- [Vistas XML para Aplicaciones Odoo](#vistas-xml-para-aplicaciones-odoo)
- [Herencia en Odoo](#herencia-en-odoo)


## Qué se debe saber del DESAROLLO Odoo 

* ¿Qué hace un desarrollador Odoo?

    * Aplicaciones y /o funcionalidades nuevas: Crear un módulo nuevo con funcionalidades nuevas en el ERP 
    * Adecuación y/o ajustes a funcionalidades existentes: Ya viene empaquetado con ciertas funcionalidades, es decir que de acuerdo a un requimrimiento se realicen cambio a las funcionalidades de ese módulo 
    * Corrección de errores: Es muy probable que algún desarrollo no funcione correctamente. 
    * Reportes 

* ¿Qué conocimientos se necesita?

    * Saber programar y/o tener lógica de programación 
    * No se requiere conocer o dominar python 

* Conocimiento básico de SQL y base de datos
    
    * En Odoo rara vez se requerirá una consulta SQL 
    * Dominar la lógica en las sentencias SQL te ayudará a entender los dominios en Odoo. 

* Lenguajes de programación que se utilizamn

    * Python
    * Xml
    * Javascript

    * Otros no tan usados
        
        * CSS
        * HTML

* La base de datos que se utiliza es PostgreSQL

* Se utiliza el ORM de Odoo para la interacción con la base de datos

* Sistema Operativo con Linux en alguna de sus distribuciones

    * Ubuntu 20.04 o superiores

* Editor de código o IDE

    * Visual Studio Code

*  Repositorio para control de versiones de código: GITHUB

* Compatibilidad con navegadores web

<h3>Consejos</h3>

* Seguir las buenas prácticas de programación 
* Sigue los lineamientos para desarrollar en Odoo 
* Conoce y aplica las convenciones de programación para python y Javascript
* Apoyate del código estándar para realizar el tuyo
* Versiona tu código con la ayuda de GitHub
* Entiende y comprende los conceptos básicos: Modelos, Campos, Vistas, Widgets
* Practica para fortalecer tu habilidad de desarrollo 
* Mantente actualizado con las nuevas novedades, versiones, widgtres, etc de Odoo 
* Sé autodidacta pero no dejes de formarte
* Capacitate

## Arquitectura y Estructura básica de una app en Odoo 

<h3>Composición de un módulo</h3>

* Objetos de negocio. Declaradas con clases Python
* Vistas de objetos: Visualización de la interfaz de usuario, declardos con archivos XML. 
* Archivos de información. 
    * Informes
    * Datos de configuración 
    * Datos de demostración
    * Y más... 
* Controladores web: Maneja solicitudes de nacegadores web 
* Datos web estáticos. Utilizados por el sitio o interfaz web 
    * Imágenes
    * Archivos CSS 
    * Javascript

<h3>Arquitectura similar a MVC</h3>

<p align="center"><img width=60% src="./Pictures/MVC.png"></p>

<h3>Estructura de una Aplicación Odoo</h3>

<p align="center"><img width=60% src="./Pictures/AplicacionOdoo.png"></p>

<h3>Archivo __init__.py</h3>

En este archivo se indicará donde se encuentran los archivos .py 

El archivo init se verá así 

```python
from . import controllers
from . import models
from . import wizards
```

Controllers, models y wizards son carpetas que creamos en nuestro proyecto. 

Dentro de las carpetas, también existe un fichero __ init __.py Y este fichero hace exactamante lo mismo, sólo que dentro de esa carpeta, es decir localiza los archivos .py e importa todos los registros que estén dentro de esa carpeta. 

<h3>Archivo __manifest__.py</h3>

Se encuentra en la carpeta principal  y nos indica donde se encuentran los archivos xml, csv y otras fuentes.

**¿Para qué sirve?**

Ene ste archivo podemos hacer la declaración de módulo y especificación de metadatos del módulo, como por ejemplo, el nombre de la alicación, descripción, sitio web de creador y de autor, versión de la aplicación del módulo, la dependencia con otros módulos, fuentes: vistas, datos, imágenes; licencia, etc. 

## Módelos Python para Aplicaciones Odoo 

<h3> Objetos de Negocio: Modelos Odoo </h3>

* Los módelos decriben objetos de negocio: Clientes, proveedores, productos, compras, etc 
* Cada modelo en odoo es declarado como una clase en python. 
* Un modelo tiene una lista de atributos y también puede definir su propia lógica de negocio. 

<p align="center"><img width=40% src="./Pictures/ModeloOdoo.png"></p>

<h3>Estructura de un Modelo</h3>

* La clase se define con **class** y se utiliza mayúscula al principio de cada palabra. 
* El nommbre del modelo se define con **_name**.
* Los campos se definen con **fields**
* Los campos se definen como atributos en la clase del modelo y definen qué puede almacenar el modelo y dónde. 

<p align="center"><img width=70% src="./Pictures/EstructuradeunModelo.png"></p>

De acuerdo al código, tenemos: 

```python
from odoo import models, fields     #Para lograr acceso a los componentes del models 

class NombreClase(models.Model):    #Declaración de la clase y se declara que sea de tipo model
    _name = 'nombre.modelo'         #Nombre del módelo

    campo1 = fields.Char()          #Campos que están dentro del módelo 
    campo2 = fields.Char()
    campo3 = fields.Char()
    campo4 = fields.Char()

    def metodo1(self):              #Finalmente, declaramos los métodos del módelo
        return self

    def metodo2(self)
        return self
```

<h3>Persistencia de datos en los Modelos</h3>

* En Odoo existe una capa de Mapeo de Objeto-Relación o ORM por sus siglas en inglés 
* El ORM de Odoo traduce instrucciones python a sentencias SQL. 
* el ORM evita escribir la mayoría de sentencias SQL y proporciona servicios de extensibilidad y seguridad
* El modelo se convierte en una tabla
* Los campos se convierten en columnas de una tabla. 

<p align="center"><img width=70% src="./Pictures/PersistenciadeDatosenlosModelos.png"></p>

<h3>Tipos de Modelo</h3>

* Los módelos de Odoo se crean heredando a ***Model,TransientModel*** o ***AbstractModel***
    * Model: Modelos regulares de BD persistentes. 
    * TransientModel: Datos temporales, almacenados en BD y automáticamente borrados de vez en cuando. 
    * AbstractModel: Sin tablas de BD vinculados a ellos. Compartidas por múltiples modelos heredados. 

## Vistas XML para Aplicaciones Odoo 

<h3>La Capa de Vista Odoo</h3>

* La capa de vista decribe la interfaz visual de usuario
* LAs vistas se definen mediante archivos XML que son utilizados por el marco del cliente web para generar vistas HTML con datos. 
* En los archivos XML se definen acciones y menús. Estos son instancias de ir.ui.view. 
* Toda vista en Odoo debe estar referenciada en el archivo __ manifest __.py en la sección data, de lo contrario Odoo no lo tomará en cuenta. 
* un mismo módelo puede tener más de una vista. 
* Existen diferentes tipos de vistas en Odoo que nos sirve para organizar nuestros campos fields de una forma lógica:
    * Vistas de tipo lista
<p align="center"><img width=70% src="./Pictures/VistasdeTipoLista.png"></p>    
    * Vistas de tipo formulario
<p align="center"><img width=60% src="./Pictures/VistasdeTipoFormulario.png"></p>
    * Vista de tipo pivote
<p align="center"><img width=60% src="./Pictures/VistasdeTipoPivote.png"></p>
    * Vista de tipo kanban
<p align="center"><img width=60% src="./Pictures/VistasdeTipoKanban.png"></p>
    * Vista de tipo búsqueda
<p align="center"><img width=30% src="./Pictures/VistasdeTipoBusqueda.png"></p>

<h3>Estructura de una Vista</h3>

* iniciamos con el tag 
```xml 
<?xml version="1.0" encoding="utf-8"?>
```
* Nuestra vista debe encontrarse entre el tag de 
```xml
<odoo></odoo>
```
* La vista se define con el tag 
```xml
<record>
``` 
al que se le tiene que especificar un **id** y el modelo **ir.ui.view**. Para el id anteponemos la palabra view, seguido del nombre del modelo y posteriormente el tipo de vista, separados por guion bajo. Ejemplo: view_nombre_modelo_tipovista.
* Se debe especificar un nombre y un modelo esto se hace con los tag 
```xml
<field></field>
```
* Se especifica el cuerpo de la vista indicando que se trata de un archivo xml 

La estructura de la vista quedará de esta manera: 

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>

    <record id="view_nombre_modelo_tipovista" model="ir.ui.view">
        <field name="name">nombre.modelo.tipovista</field>
        <field name="model">nombre.modelo</field>
        <field name="arch" type="xml">
            <!-- AQUÍ EL CONTENIDO DE LA VISTA -->
        </field>
    </record>

</odoo>
```
<h3>Estructura de un Formulario</h3>

* Para declarar un forulario se utiliza el tag 
```xml
<form></form>
```
Se puede indicar un string como título del formulario. 
* Se colocarán los botones y el widget de barra de estatus en la sección 
```xml
<header></header>.
```
* Los botones se declaran con 
```xml
<button name="nombre_funcion_python" string="Texto del boton" type="object">
```
* Los campos de estatus deben declarar con el nombre state y se utiliza el widget de barra de estaus: 
```xml
<field name="campo_estatus" widget="statusbar" readonly="1"/>
```

Continuando con el archivo XML, se introducen las líneas de la siguiente forma: 
```xml
        <field name="arch" type="xml">
            <!-- AQUÍ EL CONTENIDO DE LA VISTA, EN ESTE CASO VISTA FORMULARIO -->
            <form string="Titulo formulario">

                <header>

                    <button name="nombre_funcion_python" string="Texto del boton" type="object">
                    <field name="campo_estatus" widget="statusbar" readonly="1"/>

                </header>
            </form>
        </field>
```
<p align="center"><img width=70% src="./Pictures/VistaFormulario.png"></p>

<h3>Contenido de un formulario(sheet)</h3>

* Agregar el contenido del formulario entre los tag de 
```xml
<sheet></sheet>
```
* Se puede utilizar el tag 
```xml
<group></group>
```
Para organizar los campos dentro del formulario. Esta etiqueta inserta dos columnas y en su interior los campos se mostrarám con etiqueta. 
* Un campo y su respectiva etiqueta ocuparán dos columnas. Si dentro de group agreagamos dos secciones más de group tendremos dos columnas de campos con su respectia etiqueta. 
* El contenido del formulario se utilizan el tag **field** para colocar un campo del modelo. El campo atributo **widget** es opcional. 

```xml
<sheet>
    <!-- Contenido dividido en dos columnas. Campos con etiquetas -->
    <group>

        <!-- Contenido de la columna izquierda -->
        <group>
            <field name="nombre_campo" widget="nombre_widget"/>
        </group>

        <!-- Contenido de la columna derecha -->
        <group>
            <field name="nombre_campo2"/>
        </group>

    </group>
</sheet>
```
<p align="center"><img width=70% src="./Pictures/VistaSheet.png"></p>

<h3>Estructura de un formulario (NoteBook)</h3>

* Se llaman libretas de notas con pestañas y se utilizan para organizar un gran número de campos por tema. 
* El elemento notebook convierte las secciones en pestañas llamadas páginas. 
* Para agregar una libreta de notas con pestaña se utiliza el tag de 
```xml
<notebook></notebook>
```
* Para agregar una página se utiliza el tag 
```xml
<page></page>
```
Para el título de la página o pestaña se utiliza el atributo **String** mientras que para asginarle un nombre se utiliza el atributo **name**. 

```xml
<!-- Contenido agrupado en páginas o pestañas -->
<notebook>

    <page string="Titulo página (pestaña) 1" name="nombre_pagina">
        <!-- Contenido de la página 1 -->
    </page>

    <page string="Titulo página (pestaña) 2">
        <!-- Contenido de la página 2 -->
    </page>

</notebook>
```

<p align="center"><img width=70% src="./Pictures/VistaNotebook.png"></p>

<h3>Estructura de una Vista</h3>

* Iniciamos con el tag
```xml
<?xml version="1.0" encoding="utf-8"?>
```
* Nuestra vista ebe encontrarse entre el tag de 
```xml
<odoo></odoo>
```
* La vista se define con el tag 
```xml
<record>
```
al que se tiene que especificar un **id** y el modelo **ir.ui.view**. Para el id anteponemos la palabra view, seguido del nombre del modelo y posteriormente el tipo de vista, separados por guion bajo. Ejemplo: view_nombre_modelo_tipovista. 
* Se debe especificar un nombre y un modelo esto se hace con los tag 
```xml
<field></field>
```
* Se especifica el cuerpo de la vista indicando que se trata de un archivo xml 

La estructura de la vista quedará de esta manera: 

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>

    <record id="view_nombre_modelo_tipovista" model="ir.ui.view">
        <field name="name">nombre.modelo.tipovista</field>
        <field name="model">nombre.modelo</field>
        <field name="arch" type="xml">
            <!-- AQUÍ EL CONTENIDO DE LA VISTA -->
        </field>
    </record>

</odoo>
```

<h3>Estructura de una lista</h3>

* Para las vistas de tipo lista se utiliza el tag 
```xml
<tree></tree>
```
* Dentro del elemento tree se declaran los campos con la etiqueta 
```xml
<field>
```
* Cada elemeto field representará una columna en la tabla 

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>

    <record id="view_nombre_modelo_tipovista" model="ir.ui.view">
        <field name="name">nombre.modelo.tipovista</field>
        <field name="model">nombre.modelo</field>
        <field name="arch" type="xml">
            <!-- AQUÍ EL CONTENIDO DE LA VISTA -->

            <tree>

                <!-- Contenido a manera de columnas -->
                <field name="nombre_campo"/>
                <field name="nombre_campo2"/>

            </tree>
            
        </field>
    </record>

</odoo>
```
<p align="center"><img width=70% src="./Pictures/VistaTree.png"></p>

## Herencia en Odoo

* Nunca se debe modificar el código estándar de Odoo. 
* En lugar de sobre escribir vistas o modelos existentes, Odoo nos proporciona mecanismos para heredarlos y así extenderlos de forma modular. 
* Las herencias se utilizan para cambiar, agregar o elimiar funcionalidades existentes. Estas modificaciones pueden ser a nive modelo, vista o lógica de negocio. 
* En el archivo __ manifest __.py, en la sección **depends** se deberá indicar los módulos o aplicaciones que contienen nuestros modelos heredados.

<h3>Herencia de modelos en Odoo(_INHERIT)</h3>

* En el modelo, se sustituye la palabra reservada _name por la palabra reservada **_inherit** en la clase.
* El nombre del modelo que se declare  con _inherit debe ser un modelo ya existente. 
* Con la herencia se puede lograr: 
    * Agregar campos nuevos a un modelo existente
    * Anular la definición de campos de un modelo existente
    * Agregar restricciones o funcionalidades adicionales a un modelo existente 
    * Agregar métodos y funcionalidades nuevas a un modelo existente
    * Anular métodos o procesos a un modelo existente. 

En código, se representa así: 

```Python 
from odoo import models, fields, api

class NombreClase(models.Model):

    _inherit = 'modelo.a.heredar'

    campo adicional = fields.Char()
```

<h3>Herencia de Modelos en Odoo (Métodos)</h3>

* Una vez en un modelo heredado se puede sobreescribir por completo un método 
* Para sobreescribir un método basta con agregar el nombre del método con la misma cantidad de parametros que el método original 
* Dentro del método se puede invocar a la funcionalidad original hablando al método de la super clase. Para ello se utiliza **super(NombreClase,self).método_original()**

en código se representa así: 

```Python 
from odoo import models, fields, api 

class NombreClase(models.Model):

    _inherit = 'modelo.a.heredar'

    campo_adicional = fields.Char()

    #===================================================================#
    #   METODO_ORIGINAL(SELF)                                           #
    #   Método original en el modelo heredado 'modelo.a.heredar'        #
    #===================================================================#

    def metodo_original(self):
        # Agregar aquí funcionalidad adicional si así es requerido
        
        # Invocara método original de la superclase 'modelo.a.heredar'
        res = super(NombreClase,self).metodo_original()

        # Agregar aquí funcionalidad adicional si así es requerido

        return res
```

