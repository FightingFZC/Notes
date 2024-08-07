
# JDBC操作流程

- 使用JDBC编程需要连接数据库，注册驱动和数据库信息

- 操作Connection，打开Statement对象

- 通过Statement执行SQL，返回结果到ResultSet对象

- 使用ResultSet读取数据，然后通过代码转化为具体的POJO对象

- 关闭数据库资源

  

## 参考代码

```java

package com.iot.mybatis.jdbc;

  

//import java.sql.*;

import java.sql.Connection;

import java.sql.DriverManager;

import java.sql.PreparedStatement;

import java.sql.ResultSet;

import java.sql.SQLException;

  

/**

 * Created by Administrator on 2016/2/21.

 */

public class JdbcTest {

    public static void main(String[] args) {

        //数据库连接

        Connection connection = null;

        //预编译的Statement，使用预编译的Statement提高数据库性能

        PreparedStatement preparedStatement = null;

        //结果集

        ResultSet resultSet = null;

  

        try {

            //加载数据库驱动

            Class.forName("com.mysql.jdbc.Driver");

  

            //通过驱动管理类获取数据库链接

            connection =  DriverManager.getConnection("jdbc:mysql://120.25.162.238:3306/mybatis001?characterEncoding=utf-8", "root", "123");

            //定义sql语句 ?表示占位符

            String sql = "select * from user where username = ?";

            //获取预处理statement

            preparedStatement = connection.prepareStatement(sql);

            //设置参数，第一个参数为sql语句中参数的序号（从1开始），第二个参数为设置的参数值

            preparedStatement.setString(1, "王五");

            //向数据库发出sql执行查询，查询出结果集

            resultSet =  preparedStatement.executeQuery();

            //遍历查询结果集

            while(resultSet.next()){

                System.out.println(resultSet.getString("id")+"  "+resultSet.getString("username"));

            }

        } catch (Exception e) {

            e.printStackTrace();

        }finally{

            //释放资源

            if(resultSet!=null){

                try {

                    resultSet.close();

                } catch (SQLException e) {

                    // TODO Auto-generated catch block

                    e.printStackTrace();

                }

            }

            if(preparedStatement!=null){

                try {

                    preparedStatement.close();

                } catch (SQLException e) {

                    // TODO Auto-generated catch block

                    e.printStackTrace();

                }

            }

            if(connection!=null){

                try {

                    connection.close();

                } catch (SQLException e) {

                    // TODO Auto-generated catch block

                    e.printStackTrace();

                }

            }

  

        }

  

    }

  

}

```

## 缺点分析

- 工作量大，所有的操作都需要一步一步做。

- 需要手动处理所有异常。

  

>因此，我们需要更加方便的数据库操作框架。