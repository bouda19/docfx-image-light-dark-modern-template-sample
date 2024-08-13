# Docfx images for light and dark theme

The goal of this project is to explain how to update image based on dark and light theme of a modern [Docfx](https://dotnet.github.io/docfx/index.html) template.

## Quick implementation

Follow the official [Custom Template](https://dotnet.github.io/docfx/docs/template.html?tabs=modern#custom-template) guide to add a `main.css` CSS file into a custom template.

Supposed your light and dark images are located in the `./images` folder. Open the `main.css` and add the following content :

```{css}
#logo {
    margin-right: 10px;
}

[data-bs-theme=dark] #logo {
    content:url("../images/dark-logo.png");
}

[data-bs-theme=light] #logo {
    content:url("../images/light-logo.png");
}
```

Then run the documenation by running the following command :

```{pwsh}
docfx ./Documentation/docfx.json --serve
```

## Implementation from scratch

Install docfx

```{pwsh}
dotnet tool update -g docfx
```

Create a documentation folder

```{pwsh}
mkdir Documentation
cd .\Documentation\
```

Create a new docset

```{pwsh}
docfx init
```

Create an image folder, a custom template folder and the `main.css` CSS file.

```{pwsh}
mkdir images
mkdir my-template/public
type nul > my-template/public/main.css
```

Add the following content into the `my-template/public/main.css` CSS file

```{css}
#logo {
    margin-right: 10px;
}

[data-bs-theme=dark] #logo {
    content:url("../images/dark-logo.png");
}

[data-bs-theme=light] #logo {
    content:url("../images/light-logo.png");
}
```

Place your dark and light image into the `images` folder.

Edit the `docfx.json` file and add the following content in the `globalMetadata` section :

```{json}
"_appLogoPath": "images/dark-logo.png",
```

Adapt the `dark-logo.png` to one of your image name.

Start the docfx server

```{pwsh}
docfx --serve
```
