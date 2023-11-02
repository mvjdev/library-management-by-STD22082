# OpenAPI Specification : OAS

## Définitions : C’est une langage spécifique open-source pour les API pour rendre accessible un API à d’autres.

# Swagger Editor : C’est pouir rédiger des spécification OpenAPI
# Swagger UI : C’est pour tester les API directement depuis un navigateur
# Swagger Hub : C’est une plateforme pour concevoir des documents et deploiement des API

### Ecriture d’une spécification OAS 1
 
### On a regarder des documents , dont voici un lien de base :
### https://spec.openapis.org/oas/latest.html

### On a fait un petit rappel , avec un pratique de faire quelques requêtes sur OpenAPI v3.1.0 , tels que :		

openapi: 3.0.3
info:
  title: Library API
  version: 1.0.0
  description: STD22001
servers:
  - url: https://library.com
paths:
  /books:
    get:
      summary: Get all books
      description: The returned books are ordered by updated datetime.
      operationId: getBooks
      parameters:
        - in: query
          name: bookName
          description: Filter return books by given name
          required: false
          schema:
            type: string
        #TODO3: add parameter to filter books by intervals of dates of the releaseDate
      responses:
        200:
          description: The list of filtered books
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Book'
    put:
      summary: Create or update a list of books
      operationId: crupdateBooks
      requestBody:
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/Book'
      responses:
        200:
          description: The list of created or updated books
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Book'
  /authors:
  #TODO2: complete GET (can be filtered by name) - PUT - DELETE
components:
  schemas:
    Book:
      type: object
      properties:
        id:
          type: string
        bookName:
          type: string
        author:
          #TODO1: set it as a component with properties : id, name, sex (M or F)
          type: string
        pageNumbers:
          type: integer
        topic:
          type: string
          enum:
            - ROMANCE
            - COMEDY
            - OTHER
        releaseDate:
          type: string
          format: date
