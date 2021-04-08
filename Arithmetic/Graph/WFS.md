

## 图的最短路径

*   [前言](#preface)

*   [某个源点到其余各顶点最短路径](#)

*   [一对顶点之间最短路径](#)



<h3 id="preface">前言</h3>

在《数据结构》（严蔚敏&吴伟民）一书中花了一章节的内容来介绍图

在图的遍历一节中介绍了两种遍历方法：DFS、WFS

本篇内容主要介绍WFS的应用



![图](/Resource/2016/graph.png "图")  

    
    
    public class Dijkstra {
    
        private static final int MAX = 1024;
    
        private static final int MATRIX_LEN= 12;
    
        private static int[] dist = new int[MATRIX_LEN];
    
        private static boolean[] S = new boolean[MATRIX_LEN];
    
        private static int[] prev = new int[MATRIX_LEN];
    
        public static void main(String[] args) {
    
            int[][] dMatrix={{0,5,5,4,MAX,MAX,MAX,MAX,MAX,MAX,MAX,MAX},
                                 {5,0,MAX,MAX,MAX,MAX,MAX,MAX,3,5,MAX,MAX},
                                 {5,MAX,0,MAX,1,5,MAX,MAX,MAX,MAX,MAX,MAX},
                                 {4,MAX,MAX,0,2,MAX,MAX,MAX,3,MAX,MAX,MAX},
                                 {MAX,MAX,1,2,0,2,1,MAX,MAX,MAX,MAX,MAX},
                                 {MAX,MAX,5,MAX,2,0,2,8,MAX,MAX,MAX,MAX},
                                 {MAX,MAX,MAX,MAX,1,2,0,MAX,MAX,MAX,1,MAX},
                                 {MAX,MAX,MAX,MAX,MAX,8,MAX,0,MAX,MAX,MAX,10},
                                 {MAX,3,MAX,3,MAX,MAX,MAX,MAX,0,MAX,2,MAX},
                                 {MAX,5,MAX,MAX,MAX,MAX,MAX,MAX,MAX,0,3,10},
                                 {MAX,MAX,MAX,MAX,MAX,MAX,1,MAX,2,3,0,1},
                                 {MAX,MAX,MAX,MAX,MAX,MAX,MAX,10,MAX,10,1,0}};
    
            dijkstra(dMatrix,0);
    
        }
    
        public static void dijkstra(int[][] dMatrix,int p){
    
    
            for(int i=0; i<dMatrix.length; i++) {
    
                S[i] = false;
    
    
                dist[i]=dMatrix[p][i];
    
                if (dMatrix[p][i] == MAX) {
    
                    prev[i] = -1;
    
                } else {
    
                    prev[i] = p;
    
                }
            }
    
            dist[p] = 0;
    
            S[p] = true;
    
    
            for( int i=1; i<dMatrix.length; i++){
    
                int u = p;
    
                int min = MAX;
    
                for (int j=0; j<dMatrix.length; j++){
    
                    if( !S[j] && dist[j] < min){
    
                        u = j;
    
                        min = dist[j];
                    }
                }
    
                S[u] =true;
    
    
                for( int j=0; j<dMatrix.length; j++){
    
                    if( !S[j] && dMatrix[u][j] < MAX){
    
                        if( dist[u] + dMatrix[u][j] < dist[j] ){
    
                            dist[j] = dist[u] + dMatrix[u][j];
    
                            prev[j] = u;
                        }
                    }
                }
            }
    
        }
    
    
    }


