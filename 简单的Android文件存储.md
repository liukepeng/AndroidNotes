## 简单的Android文件存储 ##
#### 将文件存储到文件中 ####
 Context类中提供了一个`openFileOutput()`方法，可以用于将数据存储到指定的文件中。
有两个参数，第一个是文件名，不需包含路径，因为所有的文件默认存储到/data/data/package-name/files/目录下。第二个参数是文件的操作模式，主要有两种模式可选，MODE_PRIVARTE,MODE_APPEND。其中MODE_PRIVATE是默认的操作模式，表示当指定同样文件名的时候，写入的内容会将覆盖原文件的内容，而MODE_APPEND则表示如果该文件已存在，就往文件里追加内容，不存在就创建新文件。

使用`openFileOutput()`写入文件：

    public void writeToFile() {
		String content = "I want to write a file";
		FileOutputStream out = null;
		BufferedWriter writer = null;
		try {
			out = openFileOutput("KUN_DATA"， Context.MODE_PRIVATE);
			writer = new BufferedWriter(new OutputStreamWriter(out));
			writer.write(content);
		} catch (IOException) {
			e.printStackTrace();
		} finally {
			try {
				if (writer != null) {
					writer.close()；
				}
			} catch (IOException) {
				e.printStackTrace();
			}
		}
	}

#### 从文件中读取数据 ####
 Context类中还提供了一个`openFileInput()`方法，用于从文件中读取数据。只有一个参数，即文件名，也是从/data/data/package-name/files/目录下加载这个文件。
使用`openFileInput()`读取文件内容：

    public String readFromFile() {
		FileInputStream in = null;
		BufferedReader reader = null;
		StringBuilder content = new StringBuilder();
		try {
			in = openFileInput("KUN_DATA");
			reader = new BufferedReader(new InputStreamReader(in));
			String line = "";
			while ((line = reader.readLine() != null)) {
				content.append(line);
			} catch {
				e.printStackTrace();
			}
		} finally {
			if (reader != null) {
				try {
					reader.close();
				} catch {
					e.printStackTrace();
				}
			}
		}
		return content.toString();
	}