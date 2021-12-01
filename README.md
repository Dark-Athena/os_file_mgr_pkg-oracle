# os_file_mgr_pkg-oracle

项目地址：https://github.com/Dark-Athena/os_file_mgr_pkg-oracle  

os file operation,solve 18c symlink directory issue(only for linux)   
在oracle数据库中对操作系统中的文件进行读写操作，解决18c版本禁用软链接导致utl_file及bfilename报错的问题  （目前版本只能用于linux环境，windows环境没这个问题）  
以下功能均已在 12.2c/18c/21c 测试通过

```sql
  --cat a file as a varchar2 table 
  --像查询一个表一样查询操作系统上的一个文件（单列多行）
  select * from table(os_file_mgr_pkg.cat_file('XSDDIR','acl.xsd.10.2')); 
 
  --convert a soft link to real link
  --查询一个软链接目录对应的真实链接
  select os_file_mgr_pkg.GET_REAL_PATH('DATA_PUMP_DIR') from dual;


  --remove a os file by full path file name  
  --删除一个操作系统上的文件，使用全路径
  procedure rm_os_file(i_file_full_name varchar2);

  --run a os commond 
  --运行一个操作系统命令
  procedure os_cmd(i_script varchar2);

  --list dir file as a varchar2 table 
  --像查询一个表一样查询指定目录下的目录名和文件名，输出结果等同于linux命令"ls"
  select * from table(os_file_mgr_pkg.get_dir_file_list('/bin'));

  --replace directory path (only in a cdb session or non cdb)
  --使用真实路径重建数据库目录，只能在cdb会话中或者非cdb环境中运行
  procedure replace_dir_path_by_real(p_dir varchar2);
```
![image](https://user-images.githubusercontent.com/25106767/144196420-529f604c-4f07-4f64-96a6-e1e83b05efbd.png)
  
有关18c软链接的相关文章：[【ORACLE】有关18c的一个很多文章都没提到的安全方面的变更-禁止软链接](https://a.darkathena.top/archives/18c-symlink-forbid)  
