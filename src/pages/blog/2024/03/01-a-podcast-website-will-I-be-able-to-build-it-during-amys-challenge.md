---
title: Will I be able to build a piraty podcast Gatsby website during Amy's two week build challenge?
author: "@OlaHolstVea"
date: 2024-03-01
---

# I started to build a piraty podcast Gatsby website today

Will I be able to ship it during Amy's #twoweekbuild challenge?

This is what I've done so far.

```shell
gatsby init


```


```js
// template / pageTemplate.js
import React from "react";
import { graphql, Link } from "gatsby";

export default function PageTemplate({ data = {} }) {
  const { frontmatter, html } = data.markdownRemark || {};
  const { title, sections } = frontmatter || {};
  function createEmail(event) {
    event.preventDefault();
    alert("POW! You've got mail 📧 📫");
  }
  return (
    <>
      <div className="container">
        <h1>{title}</h1>
        <div dangerouslySetInnerHTML={{ __html: html }} />
        {(sections || []).map((section) => {
          const { title, subtitle, body } = section || {};
          const { html } = body?.childMarkdownRemark || {};
          const { path, label } = section.cta || {};
          const { form } = section || {};
          return (
            <section>
              {title && <h2>{title}</h2>}
              {subtitle && <h3>{subtitle}</h3>}
              {html && <div dangerouslySetInnerHTML={{ __html: html }} />}
              {path && label && <Link to={path}>{label}</Link>}
              {form && (
                <form
                  onSubmit={createEmail}
                  action="https://forms.userlist.com/b199b263-3262-435f-a9bc-96a12aa9955d/submissions"
                  method="POST"
                  acceptCharset="UTF-8"
                >
                  <fieldset>
                    <label htmlFor="fields_first_name">Your first name </label>
                    <input
                      type="text"
                      id="fields_first_name"
                      name="fields[first_name]"
                    />
                  </fieldset>
                  <fieldset>
                    <label htmlFor="fields_email">Your email address </label>
                    <input
                      type="text"
                      id="fields_email"
                      name="fields[email]"
                      required
                    />
                  </fieldset>
                  <button type="submit">
                    Subscribe to the POW! Newsletter
                  </button>
                </form>
              )}
            </section>
          );
        })}
      </div>
    </>
  );
}

export const query = graphql`
  query ($catsbyId: String) {
    markdownRemark(id: { eq: $catsbyId }) {
      html
    }
  }
`;


```







```js
// gatsby-config.js
    {
      resolve: "gatsby-source-filesystem",
      options: {
        name: "images",
        path: "./src/images/",
      },
      __key: "images",
    },
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `content`,
        path: `${__dirname}/content/`,
      },
      __key: "content",
    },
    {
      resolve: "gatsby-source-filesystem",
      options: {
        name: `markdown`,
        path: "./src/pages/",
      },
      __key: "pages",
    },


```


```js
// gatsby-node.js

const { createFilePath } = require("gatsby-source-filesystem");

async function slugifyMarkdownRemarkNode(gatsbyUtils) {
  const { actions, node, getNode } = gatsbyUtils;
  const { createNodeField } = actions;

  if (node.internal.type === "MarkdownRemark") {
    const slug = createFilePath({ node, getNode });

    createNodeField({
      name: "slug",
      node,
      value: slug,
    });
  }
}

async function bakeMarkdownNodesIntoPages({ graphql, actions }) {
  // 1. filter ☕
  //    supplies: not allMarkdownRemark.nodes 💰
  const { data } = await graphql(`
    {
      supplies: allMarkdownRemark(
        filter: { fileAbsolutePath: { regex: "/index.md/" } }
      ) {
        nodes {
          id
          fields {
            slug
          }
        }
      }
    }
  `);
  //  console.log(data);

  // 2. bakingsong 🎵 🙀
  const bakingSong = require.resolve("./src/templates/pageTemplate.js");
  // 3. aromaNode 🍰
  // Loop over the supplies.nodes and forEach((aromaNode and bake a page
  data.supplies.nodes.forEach((aromaNode) => {
    console.log(aromaNode.fields.slug, "💀📄");

    const aromaNodePath =
      aromaNode.fields.slug === "/index/" ? "/" : aromaNode.fields.slug;

    actions.createPage({
      // A. aromaNodePath 🍰.🍓.🐛
      path: aromaNodePath,

      // B. bakingSong 🎵 🙀
      component: bakingSong,

      // C. catsbyId 😼🆔
      context: {
        catsbyId: aromaNode.id,
      },
    });
  });
}
// console.log({ data });

exports.onCreateNode = async (gatsbyUtils) => {
  await Promise.all([slugifyMarkdownRemarkNode(gatsbyUtils)]);
};

exports.createPages = async (gatsbyUtils) => {
  // create pages dynamically from any data source like for example see below:
  // wait for all promises to be resolved before finishing this function
  await Promise.all([bakeMarkdownNodesIntoPages(gatsbyUtils)]);
};

```







