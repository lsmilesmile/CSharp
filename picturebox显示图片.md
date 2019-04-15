## picturebox显示图片

###### 方式一，通过打开文件夹来选择图片显示

```c#
private void button1_Click(object sender, EventArgs e)
        {
            /* 建立一个读取流  */
            OpenFileDialog Image = new OpenFileDialog();
            /* 定义路径名变量  */
            string Imagepath = string.Empty;
            /* 设定是否可以选择多个文件 */
            Image.Multiselect = true; 
            Image.Filter = "Image Files (*.tif;*.jpg;*.bmp)|*.tif;*.jpg;*.bmp";
            if (Image.ShowDialog() != DialogResult.Cancel)
            {
                try
                {
                    /* 点击后获取的图片地址 */
                    Imagepath = Image.FileName;
                    /* 通过picturebox显示出图片 */
                    pictureBox1.Load(Imagepath);
                    /* 在textbox显示路径 */
                    textBox1.Text = Imagepath; 
                }
                catch (Exception ex)
                {
                    MessageBox.Show(ex.Message);//显示报错信息 
                }
            }
            
        }
```



###### 方式二，指定路径加载。直接显示

```c#
private void button2_Click(object sender, EventArgs e)
        {
            /* 传入图片的绝对路径 */
            pictureBox1.Image = new Bitmap(@"D:\test.jpg");
            /* 让picturebox的大小适应图片 */
            pictureBox1.SizeMode = PictureBoxSizeMode.Zoom;
            /* 让图片适应pictruebox的大小 */
            pictureBox1.SizeMode = PictureBoxSizeMode.StretchImage;
        }
```

