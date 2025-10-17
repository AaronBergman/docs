# Neuronpedia Documentation

This repository contains the documentation for [Neuronpedia](https://neuronpedia.org), an open platform for mechanistic interpretability research.

**Status:** Currently being updated by Aaron to reflect Neuronpedia's latest features and improvements. This is a migration from Docusaurus to Mintlify.

## Development

Install the [Mintlify CLI](https://www.npmjs.com/package/mint) to preview your documentation changes locally. To install, use the following command:

```
npm i -g mint
```

Run the following command at the root of your documentation, where your `docs.json` is located:

```
mint dev
```

View your local preview at `http://localhost:3000`.

## Publishing changes

Install our GitHub app from your [dashboard](https://dashboard.mintlify.com/settings/organization/github-app) to propagate changes from your repo to your deployment. Changes are deployed to production automatically after pushing to the default branch.

## Need help?

For questions about Neuronpedia itself, please email [johnny@neuronpedia.org](mailto:johnny@neuronpedia.org).

### Troubleshooting

- If your dev environment isn't running: Run `mint update` to ensure you have the most recent version of the CLI.
- If a page loads as a 404: Make sure you are running in a folder with a valid `docs.json`.

### Resources
- [Neuronpedia](https://neuronpedia.org)
- [Neuronpedia Blog](https://neuronpedia.org/blog)
- [Mintlify documentation](https://mintlify.com/docs)
