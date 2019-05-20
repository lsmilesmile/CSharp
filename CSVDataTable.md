#### C#中的CSV文件操作

##### code

```c#
using System.IO;
using System.Data;
using System;


namespace CsvAndDtb
{
    /// <summary>
    /// 操作CSV文件的类
    /// </summary>
    public class CsvFileHelp
    {
        #region
        /// <summary>
        /// DataTableToCsv方法一
        /// </summary>
        /// <param name="dt">DataTable对象</param>
        /// <param name="fullPath">文件路径</param>
        public static void DataTableToCsv1(DataTable dt, string fullPath)
        {
            // fullPath - 新文件的完全限定名或相对文件名。 路径不要以目录分隔符结尾。
            FileInfo fi = new FileInfo(fullPath);
            // 判断父目录是否存在
            if (!fi.Directory.Exists)
            {
                fi.Directory.Create();
            }
            // FileStream - 给文件提供一个流，支持同步或者异步的读和写的操作
            FileStream fs = new FileStream(fullPath, System.IO.FileMode.Create, System.IO.FileAccess.Write);
            // StreamWriter - 执行一个方法，把字符以特定的编码方式写入一个流中
            StreamWriter sw = new StreamWriter(fs, System.Text.Encoding.UTF8);

            string data = "";

            // 写入列名
            // 遍历列数
            for (int i = 0; i < dt.Columns.Count; i++)
            {
                // 把每一列的列名连接到字符串data上
                data += dt.Columns[i].ColumnName.ToString();
                // 每一个列名用逗号隔开，除了最后一列的列名
                if (i < dt.Columns.Count - 1)
                {
                    data += ",";
                }
            }
            // 把一行数据写入流中
            sw.WriteLine(data);

            // 写入各行数据
            for (int i = 0; i < dt.Rows.Count; i++)
            {
                // 每次遍历都要把一行的数据存到data中，所以每次循环要清空
                data = "";
                // 遍历每行的每列
                for (int j = 0; j < dt.Columns.Count; j++)
                {
                    if (j > 0)
                    {
                        data += ",";
                    }
                    data += dt.Rows[i][j].ToString();
                }
                sw.WriteLine(data);
            }
            sw.Close();
            fs.Close();
        }
        #endregion

        #region
        /// <summary>
        /// DataTableToCsv方法二
        /// </summary>
        /// <param name="dt">DataTable对象</param>
        /// <param name="fullPath">文件路径</param>
        public static void DataTableToCsv2(DataTable dt, string fullPath)
        {
            if (dt == null || dt.Rows.Count == 0)   //确保DataTable中有数据
               return;
            string strBufferLine = "";
            StreamWriter strmWriterObj = new StreamWriter(fullPath, false, System.Text.Encoding.Default);
            //写入列头
            foreach (DataColumn col in dt.Columns)
                strBufferLine += col.ColumnName + ",";
            strBufferLine = strBufferLine.Substring(0, strBufferLine.Length - 1);
            strmWriterObj.WriteLine(strBufferLine);
            //写入记录
            for (int i = 0; i < dt.Rows.Count; i++)
            {
               strBufferLine = "";
               for (int j = 0; j < dt.Columns.Count; j++)
               {
                   if (j > 0)
                       strBufferLine += ",";
                   strBufferLine += dt.Rows[i][j].ToString().Replace(",", "");   //因为CSV文件以逗号分割，在这里替换为空
               }
               strmWriterObj.WriteLine(strBufferLine);
            }
            strmWriterObj.Close();
        }
        #endregion

        #region
        /// <summary>
        /// CsvToDataTable方法一
        /// </summary>
        /// <param name="filePath">文件路径</param>
        /// <returns>DataTable对象</returns>
        public static DataTable CsvToDataTable1(string filePath)
        {
            // 数据表对象
            DataTable dt = new DataTable();

            FileStream fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
            StreamReader sr = new StreamReader(fs, System.Text.Encoding.UTF8);
            // 每次读取的一行记录
            string strLine = "";
            // 每行记录中的各个字段
            string[] aryLine = null;
            string[] tableHead = null;
            // 列数
            int columnCount = 0;
            // 是否读取的是第一行
            bool IsFirst = true;
            // 逐行读取CSV中的数据
            while ((strLine = sr.ReadLine()) != null)  // 没读到最后一行的时候
            {
                // 如果正在读取的是第一行
                if (IsFirst == true)
                {
                    tableHead = strLine.Split(',');  // 第一行一般是列标题。把每个列字段用逗号隔开
                    IsFirst = false;  // 以后再读就不是第一行了
                    columnCount = tableHead.Length ;  // 根据字符串数组的长度确定确定列数
                    // 创建DataTable的第一列字段
                    for (int i = 0; i < columnCount; i++)
                    {
                        DataColumn dc = new DataColumn(tableHead[i]);
                        dt.Columns.Add(dc);
                    }
                }
                // 如果正在读取的不是第一行
                else
                {
                    aryLine = strLine.Split(',');
                    DataRow dr = dt.NewRow();
                    for (int j = 0; j < columnCount; j++)
                    {
                        dr[j] = aryLine[j];
                    }
                    dt.Rows.Add(dr);
                }
            }
            if (aryLine != null && aryLine.Length > 0)
            {
                dt.DefaultView.Sort = tableHead[0] + " " + "asc";
            }
            sr.Close();
            fs.Close();
            return dt;
        }
        #endregion

        #region
        /// <summary>
        /// CsvToDataTable方法二
        /// </summary>
        /// <param name="filePath">文件路径</param>
        /// <param name="n">第几行是列，一般第一行</param>
        /// <returns>DataTable对象</returns>
        public static DataTable CsvToDataTable2(string filePath, int n)
        {
            DataTable dt = new DataTable();
            StreamReader reader = new StreamReader(filePath, System.Text.Encoding.Default, false);
            int m = 0;
            // 当没有读到流的结尾
            while (!reader.EndOfStream)
            {
                m = m + 1;
                // 每行存到str中
                string str = reader.ReadLine();
                // 去掉逗号，存到字符串数组中
                string[] split = str.Split(',');
                // 如果是字段那一行
                if (m == n)
                {
                    DataColumn column;
                    for(int c = 0; c < split.Length; c++)
                    {
                        column = new DataColumn();  // 创建列
                        column.DataType = System.Type.GetType("System.String");  // 列的类型是字符串
                        column.ColumnName = split[c];
                        if (dt.Columns.Contains(split[c]))
                        {
                            column.ColumnName = split[c] + c;
                        }
                        dt.Columns.Add(column);
                    }
                }
                // 不是字段那一行
                if (m >= n + 1)
                {
                    DataRow dr = dt.NewRow();
                    for(int i = 0; i < split.Length; i++)
                    {
                        dr[i] = split[i];
                    }
                    dt.Rows.Add(dr);
                }
            }
            reader.Close();
            return dt;
        }
        #endregion

        #region
        /// <summary>
        /// 创建DataTable
        /// </summary>
        /// <returns>表对象</returns>
        public static DataTable CreateDataTable()
        {
            // 创建数据表
            DataTable table = new DataTable("testTable");
            // 创建列和行对象的变量
            DataColumn column;
            DataRow row;

            // 创建列 - 列名
            // 第一列
            column = new DataColumn();
            column.DataType = System.Type.GetType("System.String");
            column.ColumnName = "Item1";
            column.Unique = true;
            table.Columns.Add(column);

            // 第二列
            column = new DataColumn();
            column.DataType = System.Type.GetType("System.String");
            column.ColumnName = "Item2";
            column.Unique = true;
            table.Columns.Add(column);

            // 添加3行数据
            for (int i = 0; i < 3; i++)
            {
                row = table.NewRow();
                row["Item1"] = i;
                row["Item2"] = "data" + i;
                table.Rows.Add(row);
            }
            return table;
        }
        #endregion

        public static void Main(string[] args)
        {
            // 文件路径
            string fullPath = "D:\\test.csv";

            // DataTable -> CSV
            DataTable dt = CreateDataTable();  // 建一个表
            // 方法一
            DataTableToCsv1(dt, fullPath);
            // 方法二
            DataTableToCsv2(dt, fullPath);

            // CSV -> DataTable
            // 方法一
            DataTable dt = CsvToDataTable1(fullPath);
            // 方法二
            DataTable dt = CsvToDataTable2(fullPath, 1);

            // 遍历DataTable中的数据
            for (int i = 0; i < dt.Rows.Count; i++)
            {
                for (int j = 0; j < dt.Columns.Count; j++)
                {
                    Console.WriteLine(dt.Rows[i][j].ToString()); 
                }             
            } 
            Console.Read();        
        }
    }
}
```

##### testcode

```c#
using System;
using System.IO;


namespace Test
{
    class Program
    {
        #region 测试
        /// <summary>
        /// 主函数
        /// </summary>
        /// <param name="args"></param>
        public static void Main(string[] args)
        {
            string filePath = "D:\\test.csv";
            FileStream fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
            StreamReader sr = new StreamReader(fs, System.Text.Encoding.UTF8);
            // 每次读取的一行记录
            string strLine = "";  // 字符串
            // 每行记录中的各个字段
            string[] aryLine = null;  // 字符串数组
            // 逐行读取CSV中的数据
            while ((strLine = sr.ReadLine()) != null)  // 没读到最后一行的时候
            {
                // 因为读取的是csv文件，所以中间都会有“,”
                Console.WriteLine(strLine);
                // 去掉逗号，把每行每列的值存到字符串数组中
                aryLine = strLine.Split(',');
                Console.WriteLine(aryLine.Length);
            }
            sr.Close();
            fs.Close();
            Console.ReadKey();
        }
        #endregion
    }
}
```

