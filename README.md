##A parser for hive sql
###ANTLRNoCaseFileStream
this java file is a fix for the default case-sensitive parser

###Test.java
this Test-drive dependent on four regular antlr jars
1.hiveParser��ʵ����hive api����ģ�λ���ڣ�
org.apache.hadoop.hive.ql.parse.HiveParser

2.����Hive SQL����/ִ�мƻ��������̷�����
http://blog.csdn.net/wf1982/article/details/9122543

3.���ǿ���ʱֻҪimport org.apache.hadoop.hive.ql.parse.*;�͵����˴ʷ��﷨У��Ĺ����ˡ�

4.���ԾͲ�����hive����Ҫ���±���hiveparser��hivelexer�������ˡ�

5.�������hive.g�﷨�ļ��ı�д��

�������ⲹ�䣺
1.����hiveparser��hivelexer��Ҫ�õ�antlr��
���������ĸ������Ǳ����()��
    antlr-2.7.7.jar
	antlr-3.0.1.jar
	antlr-runtime-3.0.1.jar
	stringtemplate-3.1b1.jar
2.����hive.gĬ�϶Թؼ����Ǵ�Сд���еģ�����Ĭ������£�
select a from b;
�Ǵ����,
Ӧ�øĳ�;SELECT a FROM b;
�����ڵ���parserʱҪ��дһ����������
public class ANTLRNoCaseFileStream extends ANTLRFileStream {
    public ANTLRNoCaseFileStream(String fileName) throws IOException {

        super(fileName, null);

    }

    public ANTLRNoCaseFileStream(String fileName, String encoding)

    throws IOException {

        super(fileName, encoding);

    }

    public int LA(int i) {

        if (i == 0) {

            return 0; // undefined

        }

        if (i < 0) {

            i++; // e.g., translate LA(-1) to use offset 0

        }

        if ((p + i - 1) >= n) {

            return CharStream.EOF;

        }

        return Character.toUpperCase(data[p + i - 1]);

    }
}


	


