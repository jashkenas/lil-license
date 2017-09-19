fs = require 'fs'

task 'build', 'build the HTML source from the LICENSE file', ->
  source = fs.readFileSync('LICENSE').toString();
  parts = source.split('\n\n')

  html = "<div class=\"lil-license\">\n\n<h1>#{parts.shift()}</h1>\n\n"
  html += (parts.map((part) -> "<p>#{part}</p>").join('\n\n') + '\n\n</div>')

  index = fs.readFileSync('index.html').toString();
  index = index.replace(/<div class="lil-license">[\s\S]*?<\/div>/, html);
  fs.writeFileSync('index.html', index);
