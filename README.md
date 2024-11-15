# HTML to Markdown Encoder
[![Deploy static content to Pages](https://github.com/sudo-self/html2md/actions/workflows/static.yml/badge.svg)](https://github.com/sudo-self/html2md/actions/workflows/static.yml)
## <a href="https://sudo-self.github.io/html2md/">HTML2MD</a><hr>

The HTML to Markdown Converter is a web-based tool that allows users to convert HTML content into Markdown format easily. The application provides an intuitive interface for pasting HTML code, selecting conversion options, and viewing the Markdown output in real time. Users can copy the converted Markdown to their clipboard or download it as a `.md` file.

## Features

*   **Real-time Conversion:** As you type or paste HTML, the corresponding Markdown is generated instantly.
*   **Customization Options:** Choose between different heading styles, horizontal rule types, and bullet list markers for the output.
*   **Clipboard Integration:** Easily paste content from your clipboard and copy the Markdown output back to it.
*   **Downloadable Output:** Save the converted Markdown as a `.md` file with the click of a button.
*   **User-Friendly Interface:** Built using Tailwind CSS for a responsive and attractive layout.
*   **HTML Encoder:** Access an HTML encoder tool for encoding HTML entities, providing additional functionality for users.

## Technologies Used

*   **HTML5:** Structure and semantics of the webpage.
*   **CSS (Tailwind CSS):** For styling and responsive design.
*   **JavaScript:** For interactivity and conversion functionality.
*   **Turndown:** A JavaScript library for converting HTML to Markdown.
*   **Custom HTML Encoder:** Integration with an external encoder tool for encoding HTML entities.
<hr>
<img width="1440" alt="markdown" src="https://github.com/user-attachments/assets/2f707579-92ed-4d7a-b818-f75cb228f154">
<img width="1440" alt="encoder" src="https://github.com/user-attachments/assets/a0c7c575-166b-4bf5-a98f-cf12da698b04">







## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Acknowledgments

*   [Turndown](https://github.com/domchristie/turndown):&nbsp;For the HTML to Markdown conversion library.
*   [Tailwind CSS](https://tailwindcss.com/):&nbsp;For the styling framework.



## Whois-Who
1. create a new svelte project
```
npx degit sveltejs/template svelte-whois
cd svelte-whois
npm install
```
#### API KEY
```
https://whois.whoisxmlapi.com
```
#### App.svelte
(modify the default App.svelte to import WhoisLookup.svelte)
```
  import WhoisLookup from './WhoisLookup.svelte';
```
2. add it in the main component
```

<main>
  <WhoisLookup />
</main>
```
#### src/WhoisLookup.svelte
```
<script>

  import { onMount } from "svelte";

  let domain = "";
  let whoisData = null;
  let loading = false;
  let error = null;

  const fetchWhoisData = async () => {
    if (!domain) {
      error = 'Please enter a domain';
      return;
    }

    loading = true;
    error = null;

    try {

      const apiKey = "xxxxxxxxxxx";  <----API KEY HERE
      const response = await fetch(
        `https://www.whoisxmlapi.com/whoisserver/WhoisService?apiKey=${apiKey}&domainName=${domain}&outputFormat=JSON`
      );

      if (!response.ok) {
        throw new Error('Failed to fetch WHOIS data');
      }

      const data = await response.json();
      whoisData = data;
    } catch (err) {
      error = err.message || 'An error occurred';
      whoisData = null;
    } finally {
      loading = false;
    }
  };
</script>
```


#### App.svelte

```
<script>
  import WhoisLookup from './WhoisLookup.svelte';
  export let name;

  let isDarkMode = localStorage.getItem('darkMode') === 'true' ? true : false;

  const toggleDarkMode = () => {
    isDarkMode = !isDarkMode;
    localStorage.setItem('darkMode', isDarkMode);
    document.documentElement.classList.toggle('dark', isDarkMode);
  };

  document.documentElement.classList.toggle('dark', isDarkMode);
</script>

<main>
  <h1>Whois Who</h1>
  <WhoisLookup />
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    height: 100vh;
    background-color: white;
    color: black;
    transition: background-color 0.3s, color 0.3s;
  }

  main {
    text-align: center;
    width: 100%;
    padding: 1em;
    box-sizing: border-box;
  }

h1 {
  font-size: 4em;
  font-weight: 100;
  margin-bottom: 20px;
  background: linear-gradient(90deg, #e03e00, #e67e00); /* Darker shades of orange */
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}



  :global(.dark body) {
    background-color: #121212;
    color: white;
  }

  .whois-container {
    margin-top: 20px;
    padding: 10px;
    background-color: #f9f9f9;
    border: 1px dashed #ff3e00;
    max-height: 400px;
    overflow-y: auto;
  }

  :global(.dark .whois-container) {
    background-color: #333;
    color: white;
    border-color: #ff3e00;
  }

  pre {
    white-space: pre-wrap;
    word-wrap: break-word;
    font-size: 14px;
  }

.dark-button {
  background-color: transparent;
  border: none;
  padding: 10px;
  cursor: pointer;
  margin-top: 20px;
  color: black;
  font-size: 1.5rem;


  display: block;
  margin-left:  auto;
  margin-right: auto;
  text-align: center;
}


  .footer {
    position: fixed;
    bottom: 0;
    width: 100%;
    text-align: center;
    padding: 10px;
    font-size: 1rem;
    color: #ff3e00;
    font-weight: 100;
  }

  @media (max-width: 640px) {
    h1 {
      font-size: 2.5em; 
    }

    .dark-button {
      font-size: 1rem;
      padding: 8px;
    }

    .footer {
      font-size: 0.9em;
      padding: 8px;
    }
  }


  @media (min-width: 640px) {
    main {
      max-width: 700px;
    }

    h1 {
      font-size: 4em;
    }
  }
</style>
```
#### dev server 

```
npm run dev
```
#### manifest.json

```
{
  "name": "WHOIS Lookup",
  "short_name": "WHOIS",
  "description": "WHOIS Lookup - A domain info search tool.",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#ff3e00",
  "icons": [
    {
      "src": "/favicon.ico",
      "type": "image/x-icon",
      "sizes": "16x16 32x32"
    },
    {
      "src": "/icon-192.png",
      "type": "image/png",
      "sizes": "192x192"
    },
    {
      "src": "/icon-512.png",
      "type": "image/png",
      "sizes": "512x512"
    },
    {
      "src": "/icon-192-maskable.png",
      "type": "image/png",
      "sizes": "192x192",
      "purpose": "maskable"
    },
    {
      "src": "/icon-512-maskable.png",
      "type": "image/png",
      "sizes": "512x512",
      "purpose": "maskable"
    }
  ]
}
```
#### robots.txt
```
User-agent: *
Disallow:

Sitemap: https://whois.jessejesse.com/sitemap-file.xml
```
#### deploy with vercel

```
vercel --prod
```


