
# Cypress

[Cypress](https://docs.cypress.io/guides/getting-started/installing-cypress#Installing)

## Usage

```sh
# Open Tool UI
npm run cypress:open

# Run Test
npx cypress run --spec "cypress/e2e/demo/spec.cy.js" 

docker run -it -v $PWD:/e2e -w /e2e cypress/included:13.4.0
```



```yml
# e2e/docker-compose.yml from repo
# https://github.com/bahmutov/cypress-open-from-docker-compose
version: '3.2'
services:
  # this is the web application we are going to test
  sentimentalyzer:
    build: ../
    environment:
      - PORT=8123
  # Cypress container
  cypress:
    # the Docker image to use from https://github.com/cypress-io/cypress-docker-images
    image: "cypress/included:13.4.0"
    depends_on:
      - sentimentalyzer
    environment:
      # pass base url to test pointing at the web application
      - CYPRESS_baseUrl=http://sentimentalyzer:8123
    # share the current folder as volume to avoid copying
    working_dir: /e2e
    volumes:
      - ./:/e2e
```


```sh
docker-compose up --exit-code-from cypress
```
