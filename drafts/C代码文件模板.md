
C文件模板

```json
{

    // Place your 全局 snippets here. Each snippet is defined under a snippet name and has a scope, prefix, body and

    // description. Add comma separated ids of the languages where the snippet is applicable in the scope field. If scope

    // is left empty or omitted, the snippet gets applied to all languages. The prefix is what is

    // used to trigger the snippet and the body will be expanded and inserted. Possible variables are:

    // $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders.

    // Placeholders with the same ids are connected.

    // Example:

    // "Print to console": {

    //  "scope": "javascript,typescript",

    //  "prefix": "log",

    //  "body": [

    //      "console.log('$1');",

    //      "$2"

    //  ],

    //  "description": "Log output to console"

    // }

    "New project template": {

        "prefix": "project_template",

        "body": [

            "/**",

            "  *Copyright(C),2020 - 2021, Company Tech. Co., Ltd.",

            "  *FileName:   ${TM_FILENAME}",

            "  *Date:       ${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE} ${CURRENT_HOUR}:${CURRENT_MINUTE}:${CURRENT_SECOND}",

            "  *Author:     yulmx",

            "  *Version:    1.0",

            "  *Path:       ${TM_DIRECTORY}",

            "  *Description:$1",

            "**/"

        ],

        "description": "project template"

   },

   "New .c file template": {

        "prefix": "cfile_template",

        "body": [

            "/**",

            "  *Author:      yulmx",

            "**/",

            // "/* include ------------------------------------------------------------------*/",

            "#include <stdio.h>",

            "#include <stdlib.h>",

            "\n",

            // "/* private define -----------------------------------------------------------*/",

            // "\n",

            // "/* private variables --------------------------------------------------------*/",

            // "\n",

            // "/* public function prototype ------------------------------------------------*/",

            // "\n",

            // "/* private function prototype -----------------------------------------------*/"

            "int main() {", // main

            "    $0",   // 最终光标位置

            // "    system(\"pause\");",    //标准C++的等待用户动作

            "    return 0;",

            "}",

            ],

        "description": "c source file template"

    },

    "New .h file template": {

        "prefix": "hfile_template",

        "body": [

           "#ifndef ${TM_FILENAME_BASE}_H", //shift+U转换为大写

           "#define ${TM_FILENAME_BASE}_H",

           "\n\n\n\n\n\n\n\n\n\n#endif"

        ],

        "description": "c head file template"

    },

     "New c function header template": {

        "prefix": "function_template",

        "body": [

            "/**",

            "  * @brief  ${1:Desc}",

            "  * @param  ${2:None}",

            "  * @retval ${3:None}",

            "  * @note   ${4:None}",

            "*/",

            "static void ${5:function}(void)",

            "{\n\t$6\n}"

        ],

         "description": "c function header template"

    }

}
```


[VS Code自定义C代码模板_vscode c template_佛罗伦萨的阿萨辛的博客-CSDN博客](https://blog.csdn.net/weixin_42663377/article/details/109968174)


[Feather Template - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=eayer.ftemplate)