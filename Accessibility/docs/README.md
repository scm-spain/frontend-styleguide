## Documentation & TIPS

### Unidades de medida CSS: rem (propuesta)

Intentar migrar poco a poco hacia rems y relegar los px unicamente a fallback para navegadores antiguos (generarlos de manera automática, Grunt/Gulp).

#### ¿Por qué?
- Los px, a diferencia de las unidades relativas (em, rems, %), rompen algunas opciones de accesibilidad que le permiten al usuario que lo necesite configurar sus propios estilos. Por ejemplo en Google Chrome > Configuracion > Configuracion avanzada > Contenido web > Tamaño de fuente.

- Si bien es verdad que el zoom aún funciona, este funciona sobre toda la pagina, lo que puede generar scroll o descuadres indeseados en resoluciones mas pequeñas. De la otra manera tenemos mayor control, ya que sólo se afecta a los elementos que nosotros decidamos estilar con unidades relativas (por ejemplo se puede dejar font-sizes y paddings en unidades relativas pero el layout en porcentajes y pixels).

- Si todas las unidades son relativas, es muy sencillo escalar toda la web cambiando únicamente el font-size del html. Un uso claro de esto sería aumentar toda la web en las resoluciones más grandes (TVs). Ejemplo: [daverupert.com](http://daverupert.com/)

- **[Esto es opinable]** Al tratarse de numeros más pequeños las matemáticas se simplifican mucho, sobre todo si se trabaja con una escala de cuartos (4px en base 16 que es el default): 0 | 0.25 | 0.5 | 0.75 | 1 | 1.25 | 1.5 ...

        // Es mas facil alinear verticalmente esto
        .button {
            line-height: 1rem;
            margin-top: .25rem;
            padding: .5rem;
            float: left;
        }
        .logo {
            height: 2.5rem;
            float: left;
        }

        // que esto
        .button {
            line-height: 16px;
            margin-top: 4px;
            padding: 8px;
            float: left;
        }
        .logo {
            height: 40px;
            float: left;
        }


#### Recursos
- Mixin de para convertir px en rem

        $global-font-size: 100%;

        @function stripUnit($number) {
            @return $number / ($number * 0 + 1);
        }

        @function rootFontSize($html-font-size) {
            @return (stripUnit($html-font-size) * 16)/100;
        }

        @function rem($val) {
            @return (stripUnit($val) / rootFontSize($global-font-size)) + 0rem;
        }

- Task de grunt para generar fallbacks: [grunt-pixrem](https://github.com/robwierzbowski/grunt-pixrem)
