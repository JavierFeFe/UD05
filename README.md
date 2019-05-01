# TAREFA UD05

Dado o ficheiro LMSGI05_tarefa.xml, xerar un documento XHTML que mostre unha táboa segundo o formato do seguinte padrón (que se manteña o padrón do formato):

Datos	Notas
Nome	Apelidos	Tarefas	Cuestionarios	Exame	Final

Nota en letra
A nota final debe estar en letra; é dicir, se é maior ou igual a 9 será SOBRESALIENTE, se é menor que 9 e maior ou igual a 7 será NOTABLE, se está entre 7 e 6, este último incluído, será BEN, se está entre 6 e 5 será SUFICIENTE e noutro caso INSUFICIENTE.

Só se deben mostrar os datos correspondentes á convocatoria de xuño.

```Xquery
<html>
  <body>
    <table border="1">
      <tr>
        <td>Nome</td>
        <td>Apelidos</td>
        <td>Tarefas</td>
        <td>Cuestionarios</td>
        <td>Examen</td>
        <td>Final</td>
        {
        for $alumno in db:open("LMSGI05_TARE_R01")/notas/alumno
          where $alumno/@convocatoria = 'Junio'
          let $nombre := $alumno/nombre
          let $apellidos := $alumno/apellidos
          let $tarefas := $alumno/tareas
          let $cuestionarios := $alumno/cuestionarios
          let $examen := $alumno/examen
          let $final := (if (data($alumno/final) <= 5.0) then 'INSUFICIENTE'
                  else if (data($alumno/final) <= 7.0) then 'BIEN' 
                  else if (data($alumno/final) <= 9.0) then 'NOTABLE' 
                  else 'SOBRESALIENTE')
          return <tr><td>{data($nombre)}</td><td>{data($apellidos)}</td><td>{data($tarefas)}</td><td>{data($cuestionarios)}</td><td>{data($examen)}</td><td>{data($final)}</td></tr>
          
        }
      </tr>
    </table>
  </body>
</html>
```  
* RESULTADO: *
<html>
  <body>
    <table  border="1">
      <tr>
        <td>Nome</td>
        <td>Apelidos</td>
        <td>Tarefas</td>
        <td>Cuestionarios</td>
        <td>Examen</td>
        <td>Final</td>
        <tr>
          <td>Jose</td>
          <td>Muñoz Soto</td>
          <td>9.0</td>
          <td>7.0</td>
          <td>7.0</td>
          <td>NOTABLE</td>
        </tr>
        <tr>
          <td>Ana</td>
          <td>Martinez de la Fuente</td>
          <td>9.0</td>
          <td>8.0</td>
          <td>9.0</td>
          <td>NOTABLE</td>
        </tr>
        <tr>
          <td>Esther</td>
          <td>Pereda</td>
          <td>3.0</td>
          <td>2.0</td>
          <td>2.0</td>
          <td>INSUFICIENTE</td>
        </tr>
      </tr>
    </table>
  </body>
</html>
![image](https://user-images.githubusercontent.com/44543081/57030573-7439d080-6c45-11e9-923c-1ff2ff0effde.png)

