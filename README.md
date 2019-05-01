# TAREFA UD05

Dado o ficheiro LMSGI05_tarefa.xml, xerar un documento XHTML que mostre unha táboa segundo o formato do seguinte padrón (que se manteña o padrón do formato):

Datos	Notas
Nome	Apelidos	Tarefas	Cuestionarios	Exame	Final

Nota en letra
A nota final debe estar en letra; é dicir, se é maior ou igual a 9 será SOBRESALIENTE, se é menor que 9 e maior ou igual a 7 será NOTABLE, se está entre 7 e 6, este último incluído, será BEN, se está entre 6 e 5 será SUFICIENTE e noutro caso INSUFICIENTE.

Só se deben mostrar os datos correspondentes á convocatoria de xuño.

´´´Xquery
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
´´´´
