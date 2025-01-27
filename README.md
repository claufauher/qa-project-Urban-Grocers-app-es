
# Proyecto Urban Grocers - Qa Engineer TripleTen

Este proyecto consiste en una aplicación llamada Urban Grocers, de la cual, el equipo de desarrollo realizó una lista de comprobación de pruebas, por lo que este trabajo se basa en describir el proceso que nos lleva al resultado.

## Estructura del Proyecto

### Archivos y Directorios Principales

- **`.venv`**: Entorno virtual de Python que contiene las dependencias del proyecto.
- **`configuration.py`**: Archivo que gestiona configuraciones clave del proyecto.
- **`data.py`**: Archivo encargado de manejar los datos del proyecto.
- **`create_kit_test.py`**: Script para ejecutar pruebas relacionadas con un "kit".
- **`sender_stand_request.py`**: Archivo que gestiona solicitudes HTTP (para interacción con una API).

## Tecnologías Utilizadas

- **Pycharm**: Entorno de Desarrollo Integrado para trabajar con Python
- **Python**: Lenguaje de programación principal del proyecto.
- **Pytest**: Framework de pruebas utilizado para automatizar y gestionar las pruebas.
- **Requests**: Biblioteca de Python para realizar solicitudes HTTP.

## Instrucciones de Instalación

1. Clonar el repositorio del proyecto:
   ```bash
   git clone <git@github.com:lalalauchaf/qa-project-Urban-Grocers-app-es.git>
   ```
2. Navegar al directorio del proyecto:
   ```bash
   cd qa-project-Urban-Grocers-app-es
   ```
3. Crear un entorno virtual y activarlo:
   ```bash
   python -m venv .venv
   source .venv\Scripts\activate
   ```
4. Instalar la biblioteca "requests" de python:
   ```bash
   pip install requests
   ```
5. Instalar el framework "Pytest"
   ```bash
   pip install pytest
   ```

## Cómo Ejecutar el Proyecto

1. Asegúrate de estar en el entorno virtual (`.venv`).
2. Ejecutar las pruebas con pytest:
   ```bash
   pytest
   ```
 3. En el archivo "create_kit_name_kit_test.py" importar los archivos:
     ```bash
    import sender_stand_request
    import data
     ```
 4. Crea una función que cambiará el contenido del cuerpo de solicitud:
     ```bash
    def get_kit_body(name):
    current_kit_body = data.kit_body.copy()
    current_kit_body["name"] = name
    return current_kit_body
     ```
 5. Crea una función para recibir el token:
     ```bash
    def get_new_user_token():
    user_body = data.user_body
    response = sender_stand_request.post_create_new_user(user_body)
    return response.json()["authToken"]
     ```     
     
 6. Crea la lógica de las pruebas positivas (201) con la siguiente función:
     ```bash
    def positive_assert(kit_body):
    response = sender_stand_request.post_new_client_kit(kit_body, get_new_user_token())
    assert response.status_code == 201
    assert response.json()["name"] == kit_body("name")
     ```     
     
 7. Crea la lógica de las pruebas negativas (400) con la siguiente función:
     ```bash
    def negative_assert_code_400(kit_body):
    response = sender_stand_request.post_new_client_kit(kit_body, get_new_user_token())
    assert response.status_code == 400
     ```      
### Prueba n° 1

    def test1_create_kit_1_letter_in_the_name_success_response():
    current_kit_body = get_kit_body(data.test1_kit_name)
    positive_assert(current_kit_body)
    
### Prueba n° 2

    def test2_create_kit_511_letter_in_the_name_success_response():
    current_kit_body = get_kit_body(data.test2_kit_name)
    positive_assert(current_kit_body)
    
### Prueba n° 3

    def test3_create_kit_without_name():
    current_kit_body = get_kit_body(data.test3_kit_name)
    negative_assert_code_400(current_kit_body)
    
### Prueba n° 4

    def test4_create_kit_512_letter_in_the_name_unsuccess_response():
    current_kit_body = get_kit_body(data.test4_kit_name)
    negative_assert_code_400(current_kit_body)
    
### Prueba n° 5

    ddef test5_create_kit_special_characters_in_the_name_success_response():
    current_kit_body = get_kit_body(data.test5_kit_name)
    positive_assert(current_kit_body)
    
### Prueba n° 6

    def test6_create_kit_spaces_allowed_in_the_name_success_response():
    current_kit_body = get_kit_body(data.test6_kit_name)
    positive_assert(current_kit_body)
     
### Prueba n° 7

    def test7_create_kit_numbers_allowed_in_the_name_success_response():
    current_kit_body = get_kit_body(data.test7_kit_name)
    positive_assert(current_kit_body)
    
### Prueba n° 8

    def test8_create_kit_without_name_parameter():
    current_kit_body = data.kit_body.copy()
    current_kit_body.pop("name")
    negative_assert_code_400(current_kit_body)
    
### Prueba n° 9

    def test9_create_kit_different_parameter_in_the_name_unsuccess_response():
    current_kit_body = get_kit_body(data.test9_kit_name)
    negative_assert_code_400(current_kit_body)
    
## Fuentes

Fuente de documentación utilizada:
- **Documentación de la API de Urban Grocers**: se puede encontrar en el siguiente enlace https://cnt-8438828a-b6c3-48d4-943f-b29599ff7609.containerhub.tripleten-services.com/docs/


---

Claudia Faúndez, Cohorte 21, Sprint 7  
