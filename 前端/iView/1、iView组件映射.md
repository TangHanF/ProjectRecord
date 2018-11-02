在非 template/render 模式下（例如使用 CDN 引用时），组件名要分隔，例如 `DatePicker` 必须要写成 `date-picker`。

以下组件，在所有模式下，必须加前缀 `i-`，除非使用 [iview-loader](https://www.iviewui.com/docs/guide/iview-loader)：

- Switch: `i-switch`
- Circle: `i-circle`

-------



| template/render 模式 | 非 template/render 模式 |
| :------------------: | :---------------------: |
|        Button        |        i-button         |
|         Col          |          i-col          |
|        Table         |         i-table         |
|        Input         |         i-input         |
|         Form         |         i-form          |
|         Menu         |         i-menu          |
|        Select        |        i-select         |
|        Option        |        i-option         |
|       Progress       |       i-progress        |
|         Time         |         i-time          |
|       Dropdown       |        Dropdown         |
|     DropdownMenu     |      dropdown-menu      |
|       Tabs           |        Tabs             |
|     TabPane          |        tab-pane         |
|      Split           |          Split          |
|                      |                         |

