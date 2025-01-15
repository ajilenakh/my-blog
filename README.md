# My Blog Website

Welcome to my blog repository! This is a personal blog built using **Hugo**, a fast and flexible static site generator. The site leverages well-designed themes, providing a clean and modern layout. Hugo’s simplicity, speed, and ease of use make it ideal for building static websites.

## Content
- [Features](#Features)
- [Technologies Used](##Technologies_Used)
- [Setup](##Setup)
- [Contribution](##Contributing)
- [Tip](#Tip)

## Features

- **Responsive Design**: The blog is fully responsive, optimized for both desktop and mobile devices.
- **Markdown Support**: All posts are written in Markdown, making it easy to format and maintain content.
- **Hugo Themes**: Uses the [**Gokarna**](https://github.com/gokarna-theme/gokarna-hugo) Hugo theme for a beautiful and clean layout.
- **Easy Deployment**: Can be easily deployed on hosting platforms like Vercel or Netlify.

## Technologies Used

- **Hugo**: The static site generator used for building the site.
- **Markdown**: Content for the blog posts is written using Markdown.
- **Vercel**: Deployed on Vercel for fast and free hosting.

## Setup

To run this project locally, follow the steps below:

1. Clone the repository:

   ```bash
   git clone https://github.com/ajilenakh/my-blog.git && cd my-blog/
   ```
2. To run locally:
   ```bash
   hugo server
   ```
## Contributing

Contributions are welcome! If you would like to contribute to this project, please follow these steps:
- Fork the repository.
- Create a new branch (git checkout -b feature-branch).
- Make your changes.
- Commit your changes (git commit -m 'Add some feature')
- Push to the branch (git push origin feature-branch).
- Open a pull request.


## Tip

If you plan to host the site on Vercel, be aware that Vercel uses an outdated version of Hugo by default. To ensure your site builds correctly with the latest features and updates, you’ll need to manually set the Hugo version by specifying the following environment variable:

- **Key**: `HUGO_VERSION`
- **Value**: `latest` (or specify the version in this site, e.g., `0.140.2`)

You can add this environment variable in the Vercel dashboard under the project settings to ensure the build uses the correct version of Hugo.

