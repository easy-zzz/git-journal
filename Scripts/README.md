---
creation date: 2023-01-06 07:23
modification date: пятница 6-го января 2023 07:23:56
author: Ivan Yastrebov
link: https://silentvoid13.github.io/Templater/user-functions/script-user-functions.html
---

# README

> Вы всегда можете сказать настоящему другу: когда вы выставили себя дураком, он не считает, что вы выполнили постоянную работу.
> — <cite>Laurence J. Peter</cite>

## Templater

## [Функции пользователя скрипта](chrome-extension://pmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#script-user-functions)

Этот тип пользовательских функций позволяет вам вызывать функции JavaScript из файлов JavaScript и извлекать их выходные данные.

Чтобы использовать пользовательские функции скрипта, вам необходимо указать папку скрипта в настройках Templater. Эта папка должна быть доступна из вашего хранилища.

## [Определить пользовательскую функцию скрипта](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#define-a-script-user-function)

Допустим, вы указали папку `Scripts` в качестве папки вашего скрипта в настройках Templater.

Templater will load all JavaScript (`.js` files) scripts in the `Scripts` folder.

You can then create your script named `Scripts/my_script.js` (The `.js` extension is required) for example.

You will then be able to call your scripts as user functions. The function name corresponds to the script file name.

Scripts should follow the [CommonJS module specification](https://flaviocopes.com/commonjs/), and export a single function.

Let's have an example with our previous script `my_script.js`.

Note that instead of outputting directly to the console, as we did earlier, a user script needs to `return` its output:

```
function my_function (msg) {
    return `Message from my script: ${msg}`;
}
module.exports = my_function;
```

In our previous example, a complete command invocation would look like this:

```
<% tp.user.my_script("Hello World!") %>
```

Which would print `Message from my script: Hello World!` in the console.

## [Global namespace](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#global-namespace)

In script user functions, you can still access global namespace variables like `app` or `moment`.

However, you can't access the template engine scoped variables like `tp` or `tR`. If you want to use them, you must pass them as arguments for your function.

## [Functions Arguments](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#functions-arguments)

You can pass as many arguments as you want to your function, depending on how you defined it.

You can for example pass the `tp` object to your function, to be able to use all of the [internal variables / functions](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/internal-variables-functions/overview.html) of Templater: `<% tp.user.<user_function_name>(tp) %>`

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/user-functions/overview.html "Previous chapter")[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/user-functions/system-user-functions.html "Next chapter")

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/user-functions/overview.html "Previous chapter")[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/user-functions/system-user-functions.html "Next chapter")

