# MapReduce Workshop : WordCount

###   Le But de cette application comme son nom l'indique est de compter le nombre d'occurrences de chaque mot dans une base de données.
  
1-Accédez au container de namenode. . :
```console
docker exec -it namenode /bin/bash
```

2-On va créer un fichier WordCount.java avec la commande vi qui vous permet d'éditer et manipuler votre fichier texte :

```console
cat >  WordCount.java
```
- Lorsque vous exécutez cette commande, elle attendra une entrée de texte de votre part.
- Voici le code que vous devez entrer :
```console
import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
public class WordCount {
  public static class TokenizerMapper
       extends Mapper<Object, Text, Text, IntWritable>{
    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();
    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
      StringTokenizer itr = new StringTokenizer(value.toString());
      while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
      }
    }
  }
  public static class IntSumReducer
       extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();
    public void reduce(Text key, Iterable<IntWritable> values,
                       Context context
                       ) throws IOException, InterruptedException {
      int sum = 0;
      for (IntWritable val : values) {
        sum += val.get();
      }
      result.set(sum);
      context.write(key, result);
    }
  }
  public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    Job job = Job.getInstance(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
  }
}
```
![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/b41e2aee-59bc-4d5d-9ff2-395d99aa3ad3)

- Puis appuyer sur la combinaison de touches Ctrl + D (ou Ctrl + Z sur certains systèmes) pour indiquer la fin de l'entrée.

3-Compiler WordCount.java

```console
export HADOOP_CLASSPATH="/opt/hadoop-2.7.4/share/hadoop/common/hadoop-common-2.7.4.jar:/opt/hadoop-2.7.4/share/hadoop/mapreduce/hadoop-mapreduce-client-core-2.7.4.jar:/opt/hadoop-2.7.4/share/hadoop/common/lib/*:/opt/hadoop-2.7.4/share/hadoop/mapreduce/lib/*"
```
```console
export HADOOP_CLASSPATH="/opt/hadoop-2.7.4/share/hadoop/common/hadoop-common-2.7.4.jar:/opt/hadoop-2.7.4/share/hadoop/mapreduce/hadoop-mapreduce-client-core-2.7.4.jar:/opt/hadoop-2.7.4/share/hadoop/common/lib/*:/opt/hadoop-2.7.4/share/hadoop/mapreduce/lib/*"
```
- En définissant HADOOP_CLASSPATH avec ces chemins, vous indiquez au compilateur Java et aux outils Hadoop où trouver les classes nécessaires pour la compilation et l'exécution du programme WordCount.
