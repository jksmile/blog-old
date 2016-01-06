


## 【行为型】备忘录模式

*   [定义](#define)
*   [UML图](#UML)
*   [代码](#code)
*   [应用](#app)




<h3 id="define">定义</h3>

    定义：在不破坏封闭性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态，这样可以将该对象恢复至保存时的状态。

    命令模式中角色：
        1.发起人角色(Originator):负责创建一个备忘录,用以记录当前时刻它的内部状态，并可以使用备忘录恢复内部状态。发起人可以根据需要决定备忘录存储哪些内部状态
        2.备忘录角色(Memento):负责存储Originator的内部状态，并可防止Originator以外的对象访问备忘录
        3.管理者角色(Caretaker):负责保存好备忘录Memento，不能对备忘录的内容进行操作或者检查


<h3 id="UML">UML图</h3>

       _ _ __ _ _ _      _ _ _ _ _      _ __ _ _ _
      |            |    |         |    |           |
      | Originator |---→| Memento |←---| Caretaker |
      |__ _ _ _ _ _|    |_ _ _ _ _|    |_ _ _ _ _ _|



<h3 id="code">代码</h3>

    public class BankAccount{

        private String name;

        private Integer carNo;

        private Double money;

        public BankAccount(String name, Integer carNo, Double money){

            this.name = name;

            this.carNo = carNo;

            this.money = money;
        }

        //Getter And Setter.
        ...


        //Save the state.
        public Memento createMemento(){

            return new Memento(name,carNo,money);
        }

        //Recover the state.
        public void setMemento(Memento memento){

            this.name = memento.getName();

            this.carNo = memento.getCarNo();

            this.money = memento.getMoney();
        }


        public Boolean turnToOthers(Double lostMoney){

            money = money-lostMoney;

            if(money < 0){

                return false;
            }else{

                return true;
            }
        }


        @overwrite
        public void toString(){

            System.out.println(name+"-"+carNo+"-"+money);
        }
    }


***

    public class Memento{

        private String name;

        private Integer carNo;

        private Double money;

        public Memento(String name, Integer carNo, Double money){

            this.name = name;

            this.carNo = carNo;

            this.money = money;
        }

        public String getName(){

            return name;
        }

        public Integer getCarNo(){

            return carNo;
        }

        public Double getMoney(){

            return money;
        }
    }

***

    public class CareTaker{

        private Memento memento;

        public void setMemento(Memento memento){

            this.memento = memento;
        }

        public Memento getMemento(){

            return memento;
        }
    }


***

    public class Client{

        public static void main(String[] args){

            BankAccount  jk = new BankAccount("jk",6225168800198,1000.00);

            CareTaker careTaker = new CareTaker();

            careTaker.setMemento( jk.createMemento() );

            //Test case 1.
            if( jk.turnToOthers(2000) ){

                jk.toString();
            }else{

                jk.setMemento( careTaker.getMemento() );

                jk.toString();
            }

            //Test case 2.
            if( jk.turnToOthers(500) ){

                jk.toString();
            }else{

                jk.setMemento( careTaker.getMemento() );

                jk.toString();
            }


        }


    }

    运行结果：

        jk-6225168800198-1000.00

        jk-6225168800198-500.00



<h3 id="app">应用</h3>

    以上的Demo是以银行转账为例

    如果个人账户余额够转出，则打印出个人账户转出后的信息

    如果个人账户余额不够转出，刚恢复到转出前的状态并打印出账户信息


***

相关推荐：[设计模式原则](./Principle)


上一篇：[【行为型】命令模式](./Command)

下一篇：[【行为型】状态模式](./State)







