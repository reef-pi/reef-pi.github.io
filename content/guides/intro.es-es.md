---
author: "Ranjib Dey"
date: 2018-11-15
linktitle: Introduction
title: Resumen
highlight: true
weight: 1
keywords:
- reef-pi
- tanque de arrecife
- controlador
- raspberry pi
- coral
---

Esta sección proporciona una visión general del proceso de construcción y mantenimiento de un controlador reef-pi y algunos consejos y trucos sobre aspectos comunes de la construcción, como la construcción de [circuitos](/guides/electronics) o [carcasas](/guides/housing) y módulos individuales. Por favor, lea esta documentación antes de comenzar con una construcción real.

### Planificación

reef-pi es un controlador versátil y modular que permite a los usuarios personalizar su controlador según sus necesidades específicas, ajustado a su hardware y configuración de acuario particular. Decida primero las características que desea construir. Un conjunto de características objetivo puede desglosarse fácilmente en componentes necesarios y otros trabajos de construcción. El proceso de construcción implica instalar software en Raspberry Pi, soldar componentes electrónicos y fabricar una carcasa. Nada de esto es difícil de hacer, y uno definitivamente puede aprender sobre la marcha, pero el esfuerzo y el tiempo total involucrado en este proyecto dependerán en gran medida de sus habilidades y experiencias previas con proyectos similares. reef-pi está dirigido a principiantes en computadoras, electrónica y mantenimiento de arrecifes. *No necesita saber programación de software* para construir y operar reef-pi. El proceso de construcción de reef-pi requerirá herramientas para soldar circuitos, fabricar carcasas y un teclado/TV para configurar Raspberry Pi. La lista de piezas asociada con cada guía no incluye estas herramientas. Debido a la complejidad de este proyecto y las diversas partes involucradas, los errores y contratiempos son muy comunes, pero rara vez son un obstáculo insuperable. No se desanime, use la [guía de solución de problemas](/guides/troubleshooting/) cuando sea necesario. También se anima a los usuarios a hacer preguntas en su método preferido de todas las opciones disponibles (correo electrónico, foro reef2reef, problema de GitHub o canal de Slack). Generalmente, se tarda unos días a unas semanas en construir un controlador reef-pi completamente funcional. Esto no incluye el tiempo dedicado a leer/investigar o pedir los componentes. Incluya este requisito de tiempo cuando planifique su construcción. Pero vale la pena. Para la mayoría de nosotros, también ha sido una buena experiencia de aprendizaje.

### Pedir componentes

Las guías de construcción individuales de reef-pi proporcionan enlaces para comprar los componentes necesarios. Aparte de Raspberry Pi, reef-pi utiliza principalmente productos de [Adafruit](https://www.adafruit.com). Hay algunos componentes auxiliares que se obtienen de Amazon. Si está en los EE. UU., le recomiendo usar Adafruit, ya que las guías y mis construcciones personales están probadas con sus productos. Los usuarios son bienvenidos a usar alternativas (por ejemplo, diferentes proveedores o reutilizar componentes electrónicos antiguos). Cuando el software requiere un componente específico, lo indicamos explícitamente. También recomendamos encarecidamente reutilizar componentes electrónicos antiguos. reef-pi asume que los usuarios están tomando decisiones juiciosas y son conscientes de los riesgos al elegir componentes alternativos. Casi todos los componentes se pueden pedir en pasos. Los usuarios pueden comenzar solo con una Raspberry Pi y pedir componentes más adelante, trabajando de manera incremental en la construcción. Esto permite un proceso de construcción iterativo.

### Construir el controlador físico

Durante el proceso de construcción real, siga la guía de construcción específica del módulo. Consulte la [guía de circuitos](/guides/electronics) para obtener instrucciones específicas de cableado. Esta es la parte más emocionante de la construcción. Asegúrese de tener todas las herramientas necesarias (por ejemplo, soldador, kit de taladro, etc.) de antemano. Hay algunos hilos de construcción de reef-pi existentes en reef2reef a los que los usuarios pueden referirse para obtener información sobre la cadena de suministro específica de su localidad o alternativas.

A continuación se muestra una lista de guías introductorias sobre cómo construir un controlador reef-pi. Comience con la [primera guía](https://learn.adafruit.com/reef-pi-installation-and-configuration) que cubre la instalación y configuración del software y luego use las guías específicas de características individuales para construir su controlador físico. Algunas de las características, como [Auto Top Off](https://learn.adafruit.com/reef-pi-water-level-controller) o [Controlador de temperatura](https://learn.adafruit.com/reef-pi-guide-3-temperature-controller), dependen de otras características, como [Controlador de energía](https://learn.adafruit.com/reef-pi-power-controller).

- [Instalación y configuración del software](https://learn.adafruit.com/reef-pi-installation-and-configuration)
- [Controlador de energía](https://learn.adafruit.com/reef-pi-power-controller)
- [Controlador de temperatura](https://learn.adafruit.com/reef-pi-guide-3-temperature-controller)
- [Auto Top Off](https://learn.adafruit.com/reef-pi-water-level-controller)
- [Controlador de luz](https://learn.adafruit.com/reef-pi-lighting-controller)
- [Monitor de pH](https://learn.adafruit.com/reef-pi-guide-7-ph-monitoring)
- [Controlador de dosificación](https://learn.adafruit.com/reef-pi-guide-5-dosing-controller)

Además de estas guías, se proporciona documentación adicional sobre personalización y solución de problemas en la sección de [guías](/guides) aquí.

### Probar las funcionalidades que utilizará

Pruebe minuciosamente su controlador reef-pi después de que esté construido, antes de ponerlo en acción para proteger su ganado. reef-pi está en desarrollo activo y, como todo software, puede contener errores. La naturaleza de bricolaje del controlador reef-pi lo hace más vulnerable a errores e ineficiencias en el proceso, este es el riesgo que viene con su personalización. Para cada módulo, pruebe las características que utilizará y valídelo a nivel de circuito (multímetro o equivalente) y funcionalmente (adjuntando equipo de prueba, en un contenedor de agua de repuesto o tanque, etc.).

### Despliegue para instalación permanente

Una vez probado, asegure su circuito y todos los componentes electrónicos en una carcasa adecuada. Tenemos una [guía dedicada a la construcción de carcasas](/guides/housing). Recomendamos encarecidamente fijar la carcasa de reef-pi en una plataforma estable. Las opciones exactas para fijar dependerán del recinto. La mayoría de las construcciones basadas en carcasas de plástico pesan bastante menos y se pueden asegurar usando tiras de velcro en la pared o en los gabinetes de su acuario. Después de esto, su controlador reef-pi está prácticamente listo para su uso. A menos que haya algún mantenimiento o actualización de hardware, es poco probable que toque la carcasa del controlador.

### Mantenimiento y otras operaciones

reef-pi se ejecuta en Raspberry Pi, que utiliza sistemas operativos Linux. Al igual que reef-pi, Linux también está en desarrollo activo, y recomendamos a los usuarios actualizar su instalación de Linux/Raspbian trimestralmente y hacer una actualización completa del sistema operativo (nueva versión de Raspbian o Noobs, lo que sea que esté usando) al menos cada dos años. Las principales versiones de reef-pi se lanzan cada año cerca del Día de Acción de Gracias, recomendamos encarecidamente considerar la actualización de su software reef-pi durante este tiempo. Las versiones más pequeñas ocurren cada trimestre o a veces cada dos semanas (corrección de errores, características experimentales, etc. somos grandes en desarrollar pequeños pasos y lanzar con frecuencia).
Además de actualizar/actualizar el software de su construcción, es posible que necesite solucionar algunos problemas cuando encuentre alguna falla de hardware o error de software o durante el proceso de actualización/actualización de software o hardware. Tenemos [una guía dedicada a la solución de problemas](/guides/troubleshooting) que cubre los problemas más frecuentemente encontrados. Para obtener ayuda general sobre la construcción y el mantenimiento de arrecifes, use reef2reef. También lo alentamos a iniciar un hilo de construcción en reef2reef si es posible, para que otros puedan aprender de su experiencia también.