# TAREFA UD05

Dado o ficheiro LMSGI05_tarefa.xml, xerar un documento XHTML que mostre unha táboa segundo o formato do seguinte padrón (que se manteña o padrón do formato):

Datos	Notas
Nome	Apelidos	Tarefas	Cuestionarios	Exame	Final

Nota en letra
A nota final debe estar en letra; é dicir, se é maior ou igual a 9 será SOBRESALIENTE, se é menor que 9 e maior ou igual a 7 será NOTABLE, se está entre 7 e 6, este último incluído, será BEN, se está entre 6 e 5 será SUFICIENTE e noutro caso INSUFICIENTE.

Só se deben mostrar os datos correspondentes á convocatoria de xuño.

XML:
```XML
<?xml version="1.0" encoding="ISO-8859-1" standalone="yes"?>
<?xml-stylesheet type="text/xsl" href="ud05.xsl"?>
<notas>
   <alumno convocatoria="Septiembre">
      <nombre>Carlos</nombre>
      <apellidos>Amaya Arozamena</apellidos>
      <matricula>m019843</matricula>
      <cuestionarios>8.0</cuestionarios>
      <tareas>8.0</tareas>
      <examen>6.0</examen>
      <final>8.0</final>
   </alumno>
   <alumno convocatoria="Junio">
      <nombre>Jose</nombre>
      <apellidos>Muñoz Soto</apellidos>
      <matricula>m019872</matricula>
      <cuestionarios>7.0</cuestionarios>
      <tareas>9.0</tareas>
      <examen>7.0</examen>
      <final>8.5</final>
   </alumno>
   <alumno convocatoria="Junio">
      <nombre>Ana</nombre>
      <apellidos>Martinez de la Fuente</apellidos>
      <matricula>m097215</matricula>
      <cuestionarios>8.0</cuestionarios>
      <tareas>9.0</tareas>
      <examen>9.0</examen>
      <final>8.5</final>
   </alumno>
   <alumno convocatoria="Septiembre">
      <nombre>Roberto</nombre>
      <apellidos>Carrera Fernández</apellidos>
      <matricula>m059312</matricula>
      <cuestionarios>6.0</cuestionarios>
      <tareas>7.0</tareas>
      <examen>6.0</examen>
      <final>6.5</final>
   </alumno>
   <alumno convocatoria="Septiembre">
      <nombre>Concepción</nombre>
      <apellidos>Lalinde Priego</apellidos>
      <matricula>m034093</matricula>
      <cuestionarios>4.0</cuestionarios>
      <tareas>3.0</tareas>
      <examen>2.0</examen>
      <final>3.0</final>
   </alumno>
   <alumno convocatoria="Junio">
      <nombre>Esther</nombre>
      <apellidos>Pereda</apellidos>
      <matricula>m938762</matricula>
      <cuestionarios>2.0</cuestionarios>
      <tareas>3.0</tareas>
      <examen>2.0</examen>
      <final>2.5</final>
      </alumno>
</notas>

```  
XSLT:
```XSLT
<?xml version="1.0" encoding="ISO-8859-1" standalone="yes"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="2.0">
	<xsl:template match="/">
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
						<xsl:for-each select="notas/alumno[@convocatoria='Junio']">
							<tr>
								<td>
									<xsl:value-of select="nombre"/>
								</td>
								<td>
									<xsl:value-of select="apellidos"/>
								</td>
								<td>
									<xsl:value-of select="tareas"/>
								</td>
								<td>
									<xsl:value-of select="cuestionarios"/>
								</td>
								<td>
									<xsl:value-of select="examen"/>
								</td>
								<td>
									<xsl:variable name="notaFinal" select="final"/>
									<xsl:choose>
										<xsl:when test="$notaFinal &lt; 5.0">
											INSUFICIENTE
										</xsl:when>
										<xsl:when test="$notaFinal &lt; 6.0">
											SUFICIENTE
										</xsl:when>
										<xsl:when test="$notaFinal &lt; 7.0">
											BIEN
										</xsl:when>
										<xsl:when test="$notaFinal &lt; 9.0">
											NOTABLE
										</xsl:when>
										<xsl:otherwise>
											SOBRESALIENTE
										</xsl:otherwise>
									</xsl:choose>
								</td>
							</tr>
						</xsl:for-each>
					</tr>
				</table>
			</body>
		</html>
	</xsl:template>
</xsl:stylesheet>
```

