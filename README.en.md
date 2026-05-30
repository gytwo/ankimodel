# ankimodel

#### Introduction

Anki templates - including basic functions + note marking system + image cloze system [Cloze conversion + image system + marking system + outline伸缩 + card link + in-card search + popup management + citation handling]

#### Template Types

- `00-00-Underline Cloze (Single Card Multiple Cloze)`: Automatically convert underlines to cloze deletions (multiple cloze deletions on one card).
- `00-01-Standard Cloze (Multiple Cards Multiple Cloze)`: Adapted from Anki's original cloze template. Besides converting `{{text}}` to cloze deletions (multiple cards multiple cloze), it also automatically converts underlines to cloze deletions (single card multiple cloze).
- `00-02-Multiple Choice`: Automatically identifies single-choice, multiple-choice, and true/false question types. Automatically judges correct/incorrect answers, tracks time spent, and accuracy rate (resettable). On Windows, the card automatically flips after selecting an option; on mobile devices, you still need to manually tap 'Answer' to reveal the back of the card.
- `00-03-Basic`: Adapted from Anki's original Basic template.
- `00-04-Image Occlusion`: Adapted from Anki's original Image Occlusion template.

- **Notes:**
   - **Comprehensive Features:** Regardless of the template type, all include basic functions + note marking system + image cloze system features.
   - **Multi-device Synchronization:** Both the note marking system and image cloze system operate directly on card content (text/images) within the review interface. Since the Anki review interface can only read field data and cannot edit it, all operation results are temporarily stored in the local cache. Users need to manually copy the results to the corresponding Anki fields for synchronization across devices. Simply paste all markings for the current card once before exiting: copy content from the note marking system to the `NoteMarkData` field, and copy content from the image cloze system to the `ImageClozeData` field. This process can be completed independently on PC, Android, and iOS, without relying on a computer.
   - **Cloze Options:** Compared to the multi-card multiple cloze of the `00-01-Standard Cloze (Multiple Cards Multiple Cloze)` and `00-04-Image Occlusion` templates, the note marking system and image cloze system are single-card multiple cloze. However, combining these two major systems with the `00-01-Standard Cloze (Multiple Cards Multiple Cloze)` template allows for simultaneous processing of text and image layout materials. You can either create multiple cloze deletions on a single card or use `{{text/image}}` to generate multiple cards as needed.
   - **Template Selection:** The `00-01-Standard Cloze (Multiple Cards Multiple Cloze)` and `00-02-Multiple Choice` templates, covering cloze/Q&A and multiple choice question types, basically meet all needs. Whether from PDF or Word lecture notes, you can put an entire chapter into one card, learning and creating cards simultaneously (saving time by avoiding splitting large amounts of material into individual points). If you need multiple cards for memorization, switch to the editing interface and use `{{text/image}}` to add cloze deletions; otherwise, just add an underscore (underscores added in the review or editing interface are both effective). The `00-03-Basic` template only has minor style differences (suitable for short Q&A). The `00-00-Underline Cloze (Single Card Multiple Cloze)` simply avoids the issue where the `00-01-Standard Cloze (Multiple Cards Multiple Cloze)` template doesn't display the original text content when there's no cloze; other functions are identical to the `00-01-Standard Cloze (Multiple Cards Multiple Cloze)` template. The `00-04-Image Occlusion` template can only process one image at a time and is rarely used, only useful when an image contains too much content that needs to be divided into multiple cards for memorization.

#### Usage Tutorial

- **Method 1:** Copy `front` content to the Anki template front side, copy `back` content to the Anki template back side, copy `css` content to the Anki template styling (need to select the appropriate base template first and manually add the fields required by the note marking system and image cloze system).
- **Method 2:** Switch to the `anki-templates` branch, download the ZIP of the entire branch, unzip it, and import the corresponding `.apkg` files directly into Anki.

#### Basic Functions

- **Description:** The basic functions largely draw from the features and styles of the Yunshen Card Making note template, further optimized. The right column menu also applies to multiple-choice questions, but the choices are arranged horizontally.
- **Theme Switching:** 6 built-in themes; switch via the theme menu in the right column menu (if unsatisfied with the color scheme, you can modify the style section of the template).
- **Header/Footer:** Left side shows time spent, right side shows countdown [Find `var examDate = new Date("2026-08-29");` in the front/back templates and change the date to your desired date]. The center display varies slightly by template and can be modified (replace the field with your own field).
   - 00-00-Underline Cloze (Single Card Multiple Cloze): `<div class="linkRender" id="source-display">➵{{Deck}} </div>`, showing "➵Deck"
   - 00-01-Standard Cloze (Multiple Cards Multiple Cloze): `<div class="linkRender" id="source-display"> {{Deck}}➵{{Title}} </div>`, showing "Deck➵Title"
   - 00-02-Multiple Choice: `<div class="linkRender" id="source-display">{{Source}}➵{{Keyword}}</div>`, showing "Source➵Keyword"
   - 00-03-Basic: `<div class="linkRender" id="source-display">➵{{Deck}}</div>`, showing "➵Deck"
   - 00-04-Image Occlusion: `<div class="linkRender" id="source-display"> {{Deck}}➵{{Title}} </div>`, showing "Deck➵Title"
- **Cloze Conversion:** Automatically converts underscores into cloze deletions. Click the `cloze` button in the right column menu to toggle show/hide status for all cloze deletions. Click the `Nc` or `Ncloze` button to toggle show/hide status for the next cloze deletion.
- **Outline Toggle:** Automatically converts `H1-H6` into `<details><summary>` statements, achieving correct nesting and outline伸缩. Also adapts to specific Yunshen Card Making `children` structures. Click the `Expand/Collapse` button in the right column menu to expand/collapse all nodes at once. Click the `Locate` button to automatically collapse all nodes, then expand the node containing the current cloze and jump the screen to that location [only applies to the `00-01-Standard Cloze (Multiple Cards Multiple Cloze)` template]. The `+Title` button in the right column menu works with the note marking system; after adding embedded marks of type note and adding `H1-H6` embedded marks, clicking the `+Title` button can directly convert `H1-H6` in the note editor into expandable nodes.
- **Card Linking:** Enables clicking a link on one card to view the content of another card. On PC, install the `Anki Note Linker` add-on for direct use. On mobile, you need to add some code to the template and add `class="linkRender"` to the field for clickable links, which will jump to the card filter interface and automatically complete the filtering. Users need to click again to enter that card. For specific usage, refer to `https://ankiweb.net/shared/info/1077002392`. All card templates in this project have adapted this add-on, requiring no further code modification from users.
- **In-Card Search:** Click the `🔍` button in the right column menu or click the header area to pop up a search box, allowing you to search for entered text within the current card page (automatically expanding, highlighting, and locating). You can also jump directly to external links for searching. 6 built-in external links (Fenbi Public Servant/Public Institution, Xuexi Qiangguo, Accounting Standards Committee, National Laws and Regulations Database, DeepSeek). Some may require login first.
- **Popup Management:** Includes popup management for 4 specific fields (Expansion, Materials, Notes, Summary) – displayed in the menu if the field has content, click to open and view the field content. Also includes popup management for menus related to the marking system and image cloze system. All popups are scalable (drag the bottom-right corner icon), movable (click and drag the title bar), closeable by clicking outside, and stackable (active window automatically moves to the front).
- **Citation Handling:** When copying content from epub books directly into Anki using Calibre, automatically handles citation structures like `<a href="javascript:void(0)"><sup>(22)</sup></a>`, `<a href="javascript:void(0)">(22)</a>`. Adapts to Word comment structures `#_msocom_2`, `#_msoanchor_2`, Word footnote structures `#_ftn1`, `#_ftnref1`, and Word endnote structures `#_edn1`, `#_ednref1`.

#### Note Marking System

- **Description:** Allows adding note marks directly in the review interface by selecting text. Requires the additional field `NoteMarkData` for cross-device synchronization (the `🔖` icon in the top right is the entry point for the note marking system menu).
            <ul class="guide-step-list">
                <li class="guide-step-item">
            <span><strong>Usage</strong>: Select text on the page to bring up the markup toolbar, choose the desired tool to add marks. Double-click any mark to delete it. Marks do not alter the original content of Anki fields.</span>
                </li>
                <li class="guide-step-item">
            <span><strong>Markup Tools</strong>: Add Markup (HTML tags, bold, question, highlight, note) directly applies corresponding styles to the selected text. HTML tags include heading and underline tags. Setting heading tags, then clicking the heading button in the right sidebar will automatically convert them into outline format. Setting underline tags automatically converts them into cloze deletions (single card multiple cloze). Setting note tags automatically opens the note editor, allowing you to edit notes or paste rich text content.</span>
                </li>
                <li class="guide-step-item">
           <span><strong>Embedded Markups</strong>: The note editor for note marks still allows selecting text to add marks. These marks will be displayed in the note list, with a source badge after the markup type. Hovering the mouse shows the `ID` of the originating note mark. [Embedded marks are great for specific conversion purposes. For example, after adding heading tags, click the heading button in the right sidebar to convert them into outline format, then paste the entire HTML format back into the corresponding field in Anki's built-in editor to achieve a collapsed effect within the Anki editor. After conversion, you can batch delete all embedded marks added for conversion via the note list to avoid redundant marks].</span>
                </li>
                <li class="guide-step-item">
            <span><strong>Markup Navigation</strong>: Clicking on the original note text in the note list automatically jumps to the corresponding markup location; for note marks, it also automatically opens the corresponding note editor. Embedded marks cannot be directly navigated, but clicking the source badge navigates to the source note mark and opens the corresponding note editor.</span>
                </li>
                <li class="guide-step-item">
           <span><strong>Data Source</strong>: Two data sources are available, defaulting to local storage; can switch to field source [for multi-device synchronization]. Only local mode allows editing [adding, deleting]. Field data `NoteMarkData` is read-only (can be copied). When switching from field to local, you will be prompted whether to merge into local data. The merged result is: field data + local specific data.</span>
                </li>
                <li class="guide-step-item">
            <span><strong>Copy Reminder</strong>: Any editing [add, delete] operations only update local storage and cannot automatically update field data. Local storage is essentially a device cache, at risk of loss. After editing in local mode, click the `📤Cur` button to copy all data for the current card [JSON format] and manually paste it into the Anki field `NoteMarkData`. This system provides two copy formats: JSON format [`📤Cur` and `📤All`] for use as a field data source, and HTML format [`📋`] for special purposes [e.g., batch export/print].</span>
                </li>
      

#### Image Cloze System

- **Description:** Allows adding image masks, drawings, notes, etc., directly in the review interface by selecting an image. Requires the additional field `ImageClozeData` for cross-device synchronization (the `🧰` icon in the top right is the entry point for the image cloze system menu, the `🔄` icon in the top left is the restart button for the image cloze system).
        <div class="guide-card-container">
            <div class="guide-card-title blue">
                <span>🚀</span>
                <span>Core Operation Steps</span>
            </div>
            <ul class="guide-step-list">
                <li class="guide-step-item">
                    <span class="guide-step-icon">1</span>
                    <span><strong>Click Image:</strong> Activates the quick action toolbar [if clicking the image has no effect, click the restart button in the top left to restart the image system]</span>
                </li>
                <li class="guide-step-item">
                    <span class="guide-step-icon">2</span>
                    <span><strong>Select Tool:</strong> Choose pen/eraser/mask for editing [tooltips will display when hovering over any button]</span>
                </li>
                <li class="guide-step-item">
                    <span class="guide-step-icon">3</span>
                    <span><strong>Data Synchronization:</strong> After editing, click the `📤Cur` button to copy the current card's image data and paste it into the `ImageClozeData` field for cross-device synchronization</span>
                </li>
                <li class="guide-step-item">
                    <span class="guide-step-icon">4</span>
                    <span><strong>More Tools:</strong> Open the main menu [click the toolbox icon in the top right or the toolbox icon on the toolbar]. The editing tools allow you to select pen color, thickness, eraser size, and mask color. Clicking Data Management allows viewing detailed data lists [clicking a specific item automatically activates and jumps to that image, clicking the edit/add note icon after the item also automatically activates and jumps, automatically opening the note box for note editing], data statistics [overall statistics and failure list: if clicking an image yields no response and restarting the system doesn't help, please check the failure list (normal images generally do not fail)]</span>
                </li>
            </ul>
        </div>
        <div class="guide-card-container">
            <div class="guide-card-title orange">
                <span>⚠️</span>
                <span>Important Reminders</span>
            </div>
            <ul class="guide-step-list">
                <li class="guide-step-item">
                    <span class="guide-step-icon warning">!</span>
                    <span><strong>Data Source Switching:</strong> Local mode is editable, field mode is read-only. When switching from field to local, you can choose whether to merge data. The copy button on the data management panel copies data from the current data source; operations like delete, clear, etc., only affect local data and have no impact on the original field data.</span>
                </li>
                <li class="guide-step-item">
                    <span class="guide-step-icon warning">!</span>
                    <span><strong>Data Backup:</strong> Editing operations are automatically saved to local storage, no need to save manually. However, local storage is essentially a cache and at risk of loss. After editing in local mode, click the `📤Cur` [copy current card image data] and `📤All` [copy all card image data] buttons and paste into the Anki field `ImageClozeData` for backup and as a field data source [also enabling synchronization across multiple devices].</span>
                </li>
                <li class="guide-step-item">
                    <span class="guide-step-icon warning">!</span>
                    <span><strong>System Compatibility:</strong> The image system can also process images within note marks in the note marking system and will display them in the image system's data list. Clicking such an item automatically opens the note preview window for the containing note mark and automatically activates that image.</span>
                </li>
            </ul>
        </div>



#### How to Contribute

1.  Fork this repository
2.  Create a new Feat_xxx branch
3.  Commit your code
4.  Submit a Pull Request

#### Project Address

- Gitee : https://gitee.com/gytwo/ankimodel
- GitHub: https://github.com/gytwo/ankimodel