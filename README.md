# TAREFA UD05

Dado o ficheiro LMSGI05_tarefa.xml, xerar un documento XHTML que mostre unha táboa segundo o formato do seguinte padrón (que se manteña o padrón do formato):

Datos	Notas
Nome	Apelidos	Tarefas	Cuestionarios	Exame	Final

Nota en letra
A nota final debe estar en letra; é dicir, se é maior ou igual a 9 será SOBRESALIENTE, se é menor que 9 e maior ou igual a 7 será NOTABLE, se está entre 7 e 6, este último incluído, será BEN, se está entre 6 e 5 será SUFICIENTE e noutro caso INSUFICIENTE.

Só se deben mostrar os datos correspondentes á convocatoria de xuño.

Xquery:
```Xquery
<html>
  <body>
    <table border="1">
      <tr>
         <tr>
          <th colspan="3">Datos</th>
          <th colspan="3">Notas</th>
        </tr>
        <th>Nome</th>
        <th>Apelidos</th>
        <th>Tarefas</th>
        <th>Cuestionarios</th>
        <th>Examen</th>
        <th>Final</th>
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
Resultado:
```HTML
<html>
  <body>
    <table border="1">
      <tr>
        <tr>
          <th colspan="3">Datos</th>
          <th colspan="3">Notas</th>
        </tr>
        <th>Nome</th>
        <th>Apelidos</th>
        <th>Tarefas</th>
        <th>Cuestionarios</th>
        <th>Examen</th>
        <th>Final</th>
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
```

