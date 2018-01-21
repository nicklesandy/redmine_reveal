# redmine_reveal
將 Redmine wiki 內容變成簡報的模組

這模組靈感來自於 [redmine-presentation plugin](https://github.com/florentsolt/redmine-presentation)與之相容且用法大致相同.

簡報架構在非常優秀的 [revealjs](https://github.com/hakimel/reveal.js/) Javascript 函式庫.

## 最低需求

- Redmine的版本至少要 v3.0.0 以上，測試過可以運作的 Redmine 版本有 v3.1.4, v3.2.4, v3.3.3 及 v3.4.0.

## 安裝

- 安裝 `redmine_reveal` 外掛模組：

      cd $REDMINE_HOME/plugins
      git clone https://github.com/mikitex70/redmine_reveal.git

註： `$REDMINE_HOME` 為你主機Redmine的目錄，如： `/home/redmine/redmine/plugins`

- 重新啟動 Redmine 以載入 redmine_reveal 模組

## 使用

目前有五個巨集(marco)可以將 wiki 頁面轉換為簡報

安裝本外掛後，你會發現在編輯視窗的工具列上新增了幾個快速鍵，使用這些快速鍵可以讓你輕易開啟一個對話框，設定相關參數值，並將巨集插入本文中，可以幫助你快速設定巨集。

若要修改巨集，可以將編輯游標移到巨集內再按快速鍵，對話框內的會自動帶入原巨集的參數，以便做修改。

### `slide`

This macro adds a slide to the presentation. The macro body will be used as the slide body.

When the first slide is added to the page, a link `Presentation` (may be translated) will appear to the upper right corner.

Example usage:

    {{slide
    h2. Slide title

    This is the slide description:

    * can be used the normal textile syntax
    * use slide options to customize slides
    }}

    This text will not be shown in the slide.

The text outside the slide macros will still appear in the wiki page, but will not be rendered in the presentation. This can be used to insert notes/explanations in the wiki page and at the same time keep the slides clean and simple.

This previous macro example will be rendered in the wiki page as:

![Wiki page with slide](wiki_page_with_slide.png)


Notice the `Presentation` link in the upper right corner.

Once the macro in inserted in the wiki page, place the cursor somewhere in the macro and click the *Slide* toolbar button for an easy options change:

![slidesetup global options](slide_dialog_general.png)


### `subSlide`

This macro is similar to the `slide` macro, but add a so called *sub-slide* to the preceding slide.

For detail on *sub-slide* see the [revealjs documentation](https://github.com/hakimel/reveal.js/).

Example usage:

    {{slide
    }}

    {{subslide
    h2. This is the first subslide
    }}

    {{subslide
    h2. This is the second subslide
    }}

    {{subslide
    h2. This is the last subslide
    }}

Note that the main slide is empty: if you put text in the slide then it will appear in all the sub-slides. This can be used to add some common heading to the sb-slides.

### `speakerNote`

The `speakerNote` macro marks some text as to be shown in the [Speaker note window](https://github.com/hakimel/reveal.js/#speaker-notes) of the previous slide/subslide.

Speaker notes can be used to give some suggestion to the speaker on what to say, optional arguments, etc.

To show the *Speaker notes window* start the presentation and then press the `S` key.

Example usage:

    {{slide
    h2. Slide with speaker notes

    Here is the text for the presentation
    }}

    {{speakerNote
    This text is visible only in the *Speaker view*.

    * can be used any textile formatting
    }}


### `slideSetup`

This macro is used to setup some default values that can be used for all slides, instead to specify the same value for every slide.

Example usage:

    {{slideSetup(theme=beige,transition=fade)}}

Once the macro in inserted in the wiki page, place the cursor somewhere in the macro and click the *Slide setup* toolbar button for an easy options change:

![slidesetup global options](slidesetup_dialog_global.png)

Some of the options specified with the `slideSetup` macro can be overriden in the `slide` or `subslide` macros.


### `comment`

The `comment` macro can be used to hide rendering of part of the wiki page. Can be used to hide a slide, but also in all other wiki pages.

Example usage:

    {{comment
    {{slide
    h2. Hidden slide

    This slide will not be rendered.
    }}

Note that the nested macro must be closed only once: macros cannot be nested, but if for some reason you need to use a macro in a slide, the inner macro must be closed with the `}\}` sequence.
