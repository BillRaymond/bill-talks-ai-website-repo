## Create Hugo site, install and configure bootstrap
1. Create a new folder
2. Add a file and name it `Dockerfile`
3. In the Dockerfile, add `FROM billraymond/bill-talks-ai-docker-image`
4. Create a `.gitignore` file
5. In .gitignore, add `public/`
6. Run `git init` then `git commit` with the nane `initial commit`
7. Run `npm init -y`
8. Run `npm install bootstrap`
9. Run `hugo new site . --force` to create a new Hugo website
10. Run `hugo new theme bill-talks-ai` to create a new theme for the website
11. Rename the top-level `hugo.toml` to `hugo.yaml`
12. Edit the top-level `hugo.yaml` and modify the code from toml format to yaml format, filling in settings as needed, like this:
```
baseURL: 'https://bill-talks-ai.com/'
languageCode: 'en-us'
title: 'Bill Talks AI'
theme: 'bill-talks-ai'
```
13. Run `hugo` to verify the site builds without errors
14. edit the top-level `config.yaml` file, add the following lines of code toward the bottom:
```

# Process the main.js file with webpack and generate a bundled JavaScript file main.bundle.js.
module:
  mounts:
    - source: node_modules
      target: assets/node_modules
```

## Update the Hugo theme to support bootstrap
1. Edit the `themes/theme-name/layouts/partials/head.html` file and add the following code to the end of the file:
```
<!-- begin add bootstrap css assets -->
{{ $bootstrapCSS := resources.Get "/node_modules/bootstrap/dist/css/bootstrap.min.css" }}
<link rel="stylesheet" href="{{ $bootstrapCSS.Permalink }}">
<!-- end add bootstrap css assets -->
```
2. Edit the `themes/theme-name/layouts/partials/footer.html` file and add the following code to the end o the file:
```
<!-- begin add bootstrap js javascript -->
{{ $bootstrapJS := resources.Get "/node_modules/bootstrap/dist/js/bootstrap.bundle.min.js" }}
<script src="{{ $bootstrapJS.Permalink }}"></script>
<!-- end add bootstrap js javascript -->
```
3. Run `hugo` to verify there are no significant warnings or errors

## Test Bootstrap css-only AlertComponent
1. Edit the file `themes/theme-name/layouts/_default/home.html` and then add the following code immediately following `{{ define "main" }}`:
```
<!-- begin css-only bootstrap modal warning -->
<div class="alert alert-warning alert-dismissible fade show" role="alert">
  <strong>Holy guacamole!</strong> You should check out Bootstrap on your Hugo site.
  <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
</div>
<!-- Button trigger modal -->
<button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
  Launch demo modal
</button>
<!-- end css-only bootstrap modal warning -->

<!-- begin javascript modal warning -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        Welcome to Bootstrap with Hugo!
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>
<!-- end javascript modal warning -->
```
2. Run `hugo server` to verify both components function as expected. Note that the `-bs-` ensures we use BootStrap-native javascript
3. Once testing is complete, you can remove the test code

