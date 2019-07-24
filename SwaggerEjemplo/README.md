# Ejemplo Swagger

Ejemplo de generación con Swagger -> StringBoot.
Este ejemplo consta de las siguientes partes:
•	Editor de swagger (git y docker)
•	Generación de código
•	Generación de documentación HTML
•	Generación de pruebas JMeter

# Requerimientos mínimos

Java 8
Maven 3
Docker *no es obligatorio el uso de docker*

# Detalle de los sistemas

Swagger Codegen 2.3.1 (OpenApi 2.0)
Java 8
Spring-Boot 1.5.11.RELEASE
Spring-Cloud Edgware.SR3

# Preparacion

Bajar SwaggerCodeGen 2.3.1 desde nexus

Nexus
https://oss.sonatype.org
Verciones de Swagger-CodeGen
https://oss.sonatype.org/content/repositories/releases/io/swagger/swagger-codegen-cli

```bash
wget http://oss.sonatype.org/content/repositories/releases/io/swagger/swagger-codegen-cli/2.4.5/swagger-codegen-cli-2.4.5.jar -O swagger-codegen-cli.jar
```

Para editar la configuración se puede hacer de dos formas, online o local usando docket:

Para uso editor local con docker:
```bash
docker pull swaggerapi/swagger-editor
docker run -d -p 80:8080 swaggerapi/swagger-editor

Swagger editor quedara disponible en la siguiente dirección
http://127.0.0.1
```
Para uso del editor clonando editor desde GIT:

```bash
https://github.com/swagger-api/swagger-editor

git clone https://github.com/swagger-api/swagger-editor.git

swagger-editor/index.html
```

Nota: Usar la versión online solo para las pruebas, ya que el editor online deja las definiciones de API's online compartida.

Generación de código a partir de la definición y su configuración:

```bash
java -jar .\swagger-codegen-cli.jar generate -i .\swagger\api_notas.yaml -l spring -c .\swagger\config.json -o ApiNotas --ignore-file-override .\.swagger-codegen-ignore
```

Generación de la documentación a partir de la definición:

```bash
java -jar .\swagger-codegen-cli.jar generate -i .\swagger\api_notas.yaml -l html2 -o ApiNotasDoc
```

Generación de JMeter a partir de la definición:

```bash
java -jar .\swagger-codegen-cli.jar generate -i .\swagger\api_notas.yaml -l jmeter -o ApiNotasJMeter
```

Para compilar y ejecutar el proyecto son los siguientes pasos.

```bash
mvn clean package
```

Una vez compilada la API para levantar y consumir el API se debe ejecutar la siguiente instrucción:

```bash
java -jar .\target\api-notas-1.0.0.jar
```

Una levantada la API queda disponible una dirección local para consumir el API más la documentación de Swagger:

http://127.0.0.1:8080/notas