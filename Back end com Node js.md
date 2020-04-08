# Back-end com Node.js

- **Conceitos NodeJS**

    **O que é Node.js?**

    - Javascript no back-end;
        - Não lidamos com eventos do usuário final;
        - Rotas e integrações
    - Plataforma (não linguagem);
    - Construída em cima da V8;
    - Comparável a PHP / Ruby / Python / Go;

    **O que é NPM?**

    - Instalar bibliotecas de terceiros;
    - Fornecer bibliotecas;
    - Por que utilizamos Yarn?
        - Muito mais rapido
        - Yan workspaces
    - Comparáveis
        - Composer do PHP;
        - Gems do Ruby;
        - PIP do Python

    **Características do Node**  

    - Arquitetura Event-loop
        - Baseada em evento (Rotas na maioria das vezes)
        - Call Stack;
    - Node single-thread;
        - C++ por trás com libuv;
        - Background threads;
    - Non-blocking I/O

    **Frameworks**

    - ExpressJS como base:
        - Sem opinião;
        - Ótimo para iniciar;
        - Micro-serviços

    **Frameworks opinados:**

    - AdonisJS;
    - NestJS;

- **Conceitos API REST**
    - Fluxo da requisição e resposta:
        - Requisição feita por um cliente;
        - Resposta retornada através de uma estrutura de dados;
        - Cliente recebe resposta e processa resultado;

    **Como funciona?**

    - Fluxo da requisição e resposta:
        - Requisição feita por um cliente;
        - Resposta retornada através de uma estrutura de dados;
        - Cliente recebe resposta e processa resultado;
    - As rotas utilizam métodos HTTP:

            GET http://minhaapi.com/users

            POST http://minhaapi.com/users

            PUT http://minhaapi.com/users/1

            DELETE http://minhaapi.com/users/1

        GET, POST, PUT, DELETE - Métodos

        users - Recursos/Rota

        /1 - Parâmetro

    - **Benefícios**
        - Múltiplos clientes (front-end), mesmo back-end;
        - Protocolo de comunicação padronizado;
            - Mesma estrutura web / mobile / API pública
            - Comunicação com serviços externos
    - **JSON (JavaScript Object Notation)**

            {
            
            "user": {
            	"name": "Marcelo Klinher",
            	"email": "marcelo.klinger@hotmail.com",
            	"tech": ["ReactJS", "NodeJS", "React Native"],
            	"company": {
            			"name": "MK_DEV",
            			"url": "https://mkdev.com.br"
            		}
            	}
            }
            

    - **Conteúdo de requisição**

            GET http://api.com/company/1/users?page=2

    Route

    Route Params

    Query Params

        GET http://api.com/company/1/users
        
        {
        
        "user": {
        	"name": "Marcelo Klinher",
        	"email": "marcelo.klinger@hotmail.com",
        	"tech": ["ReactJS", "NodeJS", "React Native"],
        	}
        }
        {
        	"Locale": "pt_BR"
        }
        

    Body (Apenas POST/PUT)

    Headers

    **HTTP Codes**

    - 1xx: Informational
    - 2xx: Success
        - 200: Success
        - 201: CREATED
    - 3xx: Redirection
        - 301: MOVED PERMANENTLY
        - 302: MOVED
    - 4xx: Client Error
        - 400: BAD REQUEST
        - 401: UNAUTHORIZED
        - 404: NOT FOUND
    - 5xx: Server Error
        - 500: INTERNAL SERVER ERROR
    - **Criando projeto Node**

            //Criando um servidor HTTP
            //yarn init -y
            
            //yarn add express
            
            const express = require('express');
            
            const app = express();
            
            app.get('/projects', (request, response) => {
              return response.json({message: 'Hello World'})
            })
            
            app.listen(3333);

- **Configurando Nodemon**

        //yarn add nodemon -D
        //yarn nodemon src/index.js

        //package.json
        {
          "name": "backend",
          "version": "1.0.0",
          "main": "src/index.js",
          "license": "MIT",
          "scripts": {
            "dev": "nodemon"
          },
          "dependencies": {
            "express": "^4.17.1"
          },
          "devDependencies": {
            "nodemon": "^2.0.2"
          }
        }
        
        //yarn dev

- **Métodos HTTP**
    - GET - Buscar informações do Back-end

            const express = require('express');
            
            const app = express();
            
            app.get('/projects', (request, response) => {
              return response.json([
                'Project 1',
                'Project 2',
                'Project 3',
                'Project 4',
              ])
            })
            
            app.listen(3333, () => {
              console.log('back-end started');
              
            });

    - POST - Criar uma informação no Back-end

            app.post('/projects', (request, response) => {
              return response.json([
                'Project 1',
                'Project 2',
                'Project 3',
                'Project 4',
                'Project 5',
              ]);
            });

    - PUT/PATCH - Alterar uma informação no Back-end

            app.put('/projects/:id', (request, response) => {
              return response.json([
                'Project 4',
                'Project 2',
                'Project 3',
                'Project 4',
                'Project 5',
              ]);
            });

    - DELETE - Deletar uma informação no Back-end

            app.put('/projects/:id', (request, response) => {
              return response.json([
                'Project 2',
                'Project 3',
                'Project 4',
                'Project 5',
              ]);
            });

- **Utilizando o Insomnia**

    npm i insomnia-plugin-dracula-theme

    ![Back%20end%20com%20Node%20js/Captura_de_Tela_2020-04-08_s_00.37.03.png](Back%20end%20com%20Node%20js/Captura_de_Tela_2020-04-08_s_00.37.03.png)

- **Tipos de Parâmetros**
    - Tipo de parâmetros
        - Query params: Filtros e paginação

                const express = require('express');
                
                const app = express();
                
                app.get('/projects', (request, response) => {
                	const { title, owner } = request.query; 
                	//desistruturação
                	//http://localhost:3333/projects?title=projetc&owner=Marcel
                
                  return response.json([
                    'Project 1',
                    'Project 2',
                    'Project 3',
                    'Project 4',
                  ])
                })
                
                app.listen(3333, () => {
                  console.log('back-end started');
                  
                });

        - Route Params: Identificar recursos (atualizar/deletar)

                const express = require('express');
                
                const app = express();
                
                app.put('/projects/:id', (request, response) => {
                	const params = request.params;
                	//parâmetros
                
                	console.log(id)
                
                  return response.json([
                    'Project 1',
                    'Project 2',
                    'Project 3',
                    'Project 4',
                  ])
                })
                
                app.listen(3333, () => {
                  console.log('back-end started');
                  
                });

        - Request Body: Conteúdo na hora de criar ou editar um recurso (JSON)

                //insomnia
                {
                	"title": "React Native",
                	"owner": "Marcelo"
                }

                //Routas enviada em formato json
                app.use(express.json());

                const express = require('express');
                
                app.use(express.json());
                
                const app = express();
                
                app.post('/projects', (request, response) => {
                	const { title, owner } = request.body;
                
                	console.log(title) 
                	console.log(owner) 
                
                  return response.json([
                    'Project 1',
                    'Project 2',
                    'Project 3',
                    'Project 4',
                  ])
                })
                
                app.listen(3333, () => {
                  console.log('back-end started');
                  
                });

- **Aplicação Funcional**

        const express = require('express');
        const { uuid } = require('uuidv4');
        
        const app = express();
        
        app.use(express.json());
        
        const projects = [];
        
        app.get('/projects', (request, response) => {
          return response.json(projects);
        });
        
        app.post('/projects', (request, response) => {
          const { title, owner } = request.body;
        
          const project = {id: uuid(), title, owner };
        
          projects.push(projects);
        
          return response.json(project);
        });
        
        
        app.listen(3333, () => {
          console.log('back-end started');
          
        });

- **Middlewares**
    - É um interceptor de requisições, pode interromper totalmente ou alterar dados da requisição.

![Back%20end%20com%20Node%20js/Captura_de_Tela_2020-04-08_s_03.00.07.png](Back%20end%20com%20Node%20js/Captura_de_Tela_2020-04-08_s_03.00.07.png)