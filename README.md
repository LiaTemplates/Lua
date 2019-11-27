<!--
author:   André Dietrich

email:    LiaScript@web.de

version:  0.0.1

language: en

narrator: US English Male

logo:     https://upload.wikimedia.org/wikipedia/commons/thumb/c/cf/Lua-Logo.svg/480px-Lua-Logo.svg.png

comment:  A fully functional Lua-VM based on the emscripten port of
          https://daurnimator.github.io

script:   https://daurnimator.github.io/lua.vm.js/js/lua.js
          https://daurnimator.github.io/lua.vm.js/lua.vm.js


@Lua.eval
<script>
  emscripten.print = function(x) {
    console.log(x);
  }
  L.execute(`@input`)
</script>
@end
-->

# Lua - Template


                         --{{0}}--
This document defines some basic macros for applying the JavaScript Lua
interpreter and VM https://daurnimator.github.io in
[LiaScript](https://LiaScript.github.io) to make Markdown code-blocks
executable.

__Try it on LiaScript:__

https://liascript.github.io/course/?https://raw.githubusercontent.com/liaTemplates/Lua/master/README.md

__See the project on Github:__

https://github.com/liaTemplates/Lua

                         --{{1}}--
There are three ways to use this template. The easiest way is to use the
`import` statement and the URL of the raw text-file of the master branch or any
other branch or version. But you can also copy the required functionality
directly into the header of your Markdown document, see therefor the
[last slide](#3). And of course, you could also clone this project and change
it, as you wish.

                           {{1}}
1. Load the macros via

   `import: https://raw.githubusercontent.com/liaTemplates/Lua/master/README.md`

2. Copy the definitions into your Project

3. Clone this repository on GitHub

## `@LUA.eval`

                         --{{0}}--
Add the macro `@LUA.eval` to the end of a single Lua code-block to make it
executable and editable in LiaScript. The current code gets evaluate by the
JavaScript Lua interpreter and the result is shown in a console below.


``` lua
print('hello' .. ' ' .. 'world!') -- This is Lua!

print(js.global:eval('[0,1,2,3,4,5][3]')) -- Run JS from Lua

-- Interact with the page using Lua

local screen = js.global.screen
print("you haz " .. (screen.width*screen.height) .. " pixels")

local window = js.global -- global object in JS is the window
window:alert("hello from lua!")
window:setTimeout(function() print('hello from lua callback') end, 2500)

local document = js.global.document
print("this window has title '" .. document.title .. "'")

-- call constructors (global, or as properties of other objects)
print("i made an ArrayBuffer of size " .. js.new(js.global.ArrayBuffer, 20).byteLength)
-- print("i made an ArrayBuffer of size " .. js.global.ArrayBuffer:new(20).byteLength)

print("time iz " .. js.global.Date.now()) -- call with no arguments

print('done!')
```
@Lua.eval


## Implementation

                         --{{0}}--
The code shows how the macro is implemented by calling the macro `@Lua.eval`.
The `@input` macro gets substituted by the current input code. The script
commands at the top define the references to the Lua JavaScript implementations
that need to be called to load the interpreter and VM.

``` js
script:   https://daurnimator.github.io/lua.vm.js/js/lua.js
          https://daurnimator.github.io/lua.vm.js/lua.vm.js


@Lua.eval
<script>
  emscripten.print = function(x) {
    console.log(x);
  }
  L.execute(`@input`)
</script>
@end
```

                         --{{1}}--
If you want to minimize loading effort in your LiaScript project, you can also
copy this code and paste it into your main comment header, see the code in the
raw file of this document.

{{1}} https://raw.githubusercontent.com/liaTemplates/Lua/master/README.md
