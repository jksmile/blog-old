

## 【结构型】组合模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：将对象组合成树形结构以表示‘部分-整体’的 层次结构。组合模式使得用户对单个对象和组合对象的使用具有一致性。
    
    代理模式几个角色：
        1.抽象构件角色：组合中对象声明接口，在适当情况下，实现所有类共有的默认行为。声明一个接口用于访问和管理子部件
        2.树叶构件角色：在组合树中表示叶节点对象，叶节点没有子节点
        3.树枝构件角色：定义有子部件的那些部件的行为。存储子部件，在抽象构件角色中实现与子部件有关的操作



<h3 id="UML">UML图</h3>


                
                
      _  _ _ _       _ _ _ _ _ _
     |        |     |           |
     | Client |----→| Component |←------------┐
     |_  _ _ _|     |_ _ _ _ _ _|             |
                          ↑                   |
                          |                   |
                          |                   |
                ┌----------------┐            |
                |                |            |
                |                |            |
                |                |            |
           _ _  _ _          _ _ |_ _ _ _ _   |children
          |  Leaf  |        | Composite    |--┘
          |_ _ _ _ |        |_ _ _ _ __ _ _|

<h3 id="code">代码</h3>

    abstract class CompanyGroup{

        protected String name;

        protected int employeeNum;


        public void setLeaderName(String name, int employeeNum){

            this.name = name;

            this.employeeNum = employeeNum;
        }

        public abstract void addSubCompany(CompanyGroup companyGroup);


        public abstract void  employeeNum();

    }


***

    public class company extends CompanyGroup{

        public company(String name, int num){

            super(name,num);
        }

        @override
        public void addSubCompany(CompanyGroup companyGroup){

            //Nothing do do.
        }

        @override
        public void employeeNum(){

            System.out.println(this.name+" have "+this.employeeNum+" employees.");

        }

    }


***

    public class CompanyCN extends CompanyGroup{

        private List<CompanyGroup> companyList = new ArrayList<CompanyGroup>();


        public CompanyCN(String name, int num){

            super(name,num);
        }


        @override
        public void addSubCompany(CompanyGroup companyGroup){

            companyList.add(companyGroup);
        }


        @override
        public void employeeNum(){


            for(CompanyGroup company in companyList){

                company.employeeNum();
            }

            System.out.println(this.name+" have "+this.employeeNum+" employees.");

        }


    }

***

    public class Client{


        public static void main(String[] args){

            CompanyGroup companyCN = new CompanyCN("ChinaCN",100);

            companyCN.add(new Company("bj",50);

            companyCN.add(new Company("sh",50);


            companyCN.employeeNum();


        }

    }

    运行结果：

        bj have 50 employees.

        sh have 50 employees.

        ChinaCN have 100 employees.



<h3 id="app">应用</h3>



***

相关推荐：[设计模式原则](./Principle)


上一篇：[【结构型】桥接模式](./Bridge)

下一篇：[【结构型】享元模式](./Flyweight)







