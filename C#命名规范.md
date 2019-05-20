#### C#命名规范

##### 与类相关

| 标识符           | 大小写 | 示例                                                   |
| ---------------- | ------ | ------------------------------------------------------ |
| 类/结构          | Pascal | AppDomain                                              |
| 枚举类型         | Pascal | ErrorLevel                                             |
| 枚举值           | Pascal | FatalError                                             |
| 事件             | Pascal | ValueChange                                            |
| 异常类           | Pascal | WebException 注意 总是以 Exception 后缀结尾。          |
| 只读的静态字段   | Pascal | RedValue                                               |
| 接口             | Pascal | IDisposable 注意 总是以 I 前缀开始。                   |
| 集合             | Pascal | CustomerCollection 注意 总是以Collection结束           |
| 方法             | Pascal | ToString                                               |
| 命名空间         | Pascal | System.Drawing                                         |
| 参数             | Camel  | typeName                                               |
| 属性             | Pascal | BackColor                                              |
| 受保护的实例字段 | Camel  | redValue 注意 很少使用。属性优于使用受保护的实例字段。 |
| 公共实例字段     | Pascal | RedValue 注意 很少使用。属性优于使用公共实例字段。     |

##### 与变量命名相关

| 类型     | 前缀 | 示例               |
| -------- | ---- | ------------------ |
| Array    | arr  | arrShoppingList    |
| Boolean  | bln  | blnIsPostBack      |
| Byte     | byt  | bytPixelValue      |
| Char     | chr  | chrDelimiter       |
| DateTime | dtm  | dtmStartDate       |
| Decimal  | dec  | decAverageHeight   |
| Double   | dbl  | dblSizeofUniverse  |
| Integer  | int  | intRowCounter      |
| Long     | lng  | lngBillGatesIncome |
| Object   | obj  | objReturnValue     |
| Short    | shr  | shrAverage         |
| Single   | sng  | sngMaximum         |
| String   | str  | strFirstName       |

##### 与ADO.NET相关

| 数据类型     | 数据类型简写 | 标准命名举例        |
| ------------ | ------------ | ------------------- |
| Connection   | con          | conNorthwind        |
| Command      | cmd          | cmdReturnProducts   |
| Parameter    | parm         | parmProductID       |
| DataAdapter  | dad          | dadProducts         |
| DataReader   | dtr          | dtrProducts         |
| DataSet      | dst          | dstNorthWind        |
| DataTable    | dtbl         | dtblProduct         |
| DataRow      | drow         | drowRow98           |
| DataColumn   | dcol         | dcolProductID       |
| DataRelation | drel         | drelMasterDetail    |
| DataView     | dvw          | dvwFilteredProducts |

##### 与页面控件有关

| 数据类型          | 数据类型简写 | 标准命名举例 |
| ----------------- | ------------ | ------------ |
| Label             | lbl          | lblMessage   |
| LinkLabel         | llbl         | llblToday    |
| Button            | btn          | btnSave      |
| TextBox           | txt          | txtName      |
| MainMenu          | mmnu         | mmnuFile     |
| CheckBox          | chk          | chkStock     |
| RadioButton       | rbtn         | rbtnSelected |
| GroupBox          | gbx          | gbxMain      |
| PictureBox        | pic          | picImage     |
| Panel             | pnl          | pnlBody      |
| DataGrid          | dgrd         | dgrdView     |
| ListBox           | lst          | lstProducts  |
| CheckedListBox    | clst         | clstChecked  |
| ComboBox          | cbo          | cboMenu      |
| ListView          | lvw          | lvwBrowser   |
| TreeView          | tvw          | tvwType      |
| TabControl        | tctl         | tctlSelected |
| DateTimePicker    | dtp          | dtpStartDate |
| HscrollBar        | hsb          | hsbImage     |
| VscrollBar        | vsb          | vsbImage     |
| Timer             | tmr          | tmrCount     |
| ImageList         | ilst         | ilstImage    |
| ToolBar           | tlb          | tlbManage    |
| StatusBar         | stb          | stbFootPrint |
| OpenFileDialog    | odlg         | odlgFile     |
| SaveFileDialog    | sdlg         | sdlgSave     |
| FoldBrowserDialog | fbdlg        | fgdlgBrowser |
| FontDialog        | fdlg         | fdlgFoot     |
| ColorDialog       | cdlg         | cdlgColor    |
| PrintDialog       | pdlg         | pdlgPrint    |

| 数据类型               | 简写 | 举例                 |
| ---------------------- | ---- | -------------------- |
| AdRotator              | adrt | Example              |
| Button                 | btn  | btnSubmit            |
| Calendar               | cal  | calMettingDates      |
| CheckBox               | chk  | chkBlue              |
| CheckBoxList           | chkl | chklFavColors        |
| CompareValidator       | valc | valcValidAge         |
| CustomValidator        | valx | valxDBCheck          |
| DataGrid               | dgrd | dgrdTitles           |
| DataList               | dlst | dlstTitles           |
| DropDownList           | drop | dropCountries        |
| HyperLink              | lnk  | lnkDetails           |
| Image                  | img  | imgAuntBetty         |
| ImageButton            | ibtn | ibtnSubmit           |
| Label                  | lbl  | lblResults           |
| LinkButton             | lbtn | lbtnSubmit           |
| ListBox                | lst  | lstCountries         |
| Panel                  | pnl  | pnlForm2             |
| PlaceHolder            | plh  | plhFormContents      |
| RadioButton            | rad  | radFemale            |
| RadioButtonList        | radl | radlGender           |
| RangeValidator         | valg | valgAge              |
| Regularexpression_r    | vale | valeEmail_Validator  |
| Repeater               | rpt  | rptQueryResults      |
| RequiredFieldValidator | valr | valrFirstName        |
| Table                  | tbl  | tblCountryCodes      |
| TableCell              | tblc | tblcGermany          |
| TableRow               | tblr | tblrCountry          |
| TextBox                | txt  | txtFirstName         |
| ValidationSummary      | vals | valsFormErrors       |
| XML                    | xmlc | xmlcTransformResults |

```
私有成员变量一般加下划线 "_",如private int _location;
```

