# gatsby-transformer-plaintext

Adds PlainText nodes to gatsby. Every file with a **.txt** extension or without a file extension will be added as PlainText node.

## Install

`npm install --save gatsby-transformer-plaintext`

**Note:** You also need to have `gatsby-source-filesystem` installed and configured so it points to your files.

## How to use

In your `gatsby-config.js`

```javascript
module.exports = {
  plugins: [
    `gatsby-transformer-plaintext`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `./src/data/`,
      },
    },
  ],
}
```

Where the _source folder_ `./src/data/` contains plain text files such as `LICENSE`.

## How to query

You can query the nodes using GraphQL, like from the GraphiQL browser: `http://localhost:8000/___graphql`.

### Query all plain text files

```graphql
{
  allPlainText {
    nodes {
      content
    }
  }
}
```

Returns:

```json
{
  "data": {
    "allPlainText": {
      "nodes": [
        {
          "content": "content of file"
        },
        {
          "content": "content of second file"
        }
      ]
    }
  }
}
```

### Query a specific plain text file

```graphql
{
  file(relativePath: { eq: "LICENSE" }) {
    childPlainText {
      content
    }
  }
}
```

Returns:

```json
{
  "data": {
    "file": {
      "childPlainText": {
        "content": "MIT License"
      }
    }
  }
}
```