

## 【分配排序】基数排序


*   [前言](#pre)

*   [思想](#idea)

*   [Code](#code)



<h3 id="pre">前言</h3>

----

    Waiting for update...


<h3 id="idea">思想</h3>

----

示例数组A

    | 12 | 8 | 132 | 29 | 76 | 48 | 7 |


计算出数组A中最大元素a，确定最大元素长度n

建立一个长度为10的数组X，数组中的元素是同样是一个数组，如果数组A中元素个位数字x,则将元素放入数组X中的x位置

    | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
              ↓               ↓   ↓   ↓   ↓
              12              76  7   8   29
              ↓                       ↓
              132                     48

循环数组X，将数组X中元素长度大于0的项，依次取出重新放入数组A中，并且清空数组X，待下次使用

    | 12 | 132 | 76 | 7 | 8 | 48 | 29 |



取数组A中十位数字x，将元素放入数组X中的x位置,如果元素小于10，十位则为0

    | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
      ↓   ↓   ↓   ↓   ↓           ↓
      7   12  29 132  48          76
      ↓
      8

循环数组X，将数组X中元素长度大于0的项，依次取出放入数组A中，并且清空数组X，待下次使用

    | 7 | 8 | 12 | 29 | 132 | 48 | 76 |



取数组A中百位数字x，将元素放入数组X中的x位置,如果元素小于100，百位则为0

    | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
      ↓   ↓
      7   132
      ↓
      8
      ↓
      12
      ↓
      29
      ↓
      48
      ↓
      76

循环数组X，将数组X中元素长度大于0的项，依次取出放入数组A中，并且清空数组X，待下次使用

    | 7 | 8 | 12 | 29 | 48 | 76 | 132 |


到此，最大位长度已经循环完毕，排序完成！




<h3 id="code">code</h3>

----

    public class RadixSort {

        private static int maxNumLen;


        public static void main(String[] args) {

            int[] arr={12,8,132,29,76,48,7};

            maxNumLen = findMaxNumLen(arr);

            for(int i=1; i<=maxNumLen; i++){

                radixSort(arr,i);
            }
        }


        public static int findMaxNumLen(int[] arr){

            int tmp = arr[0];

            for(int i=1; i<arr.length; i++){

                if(arr[i] > tmp) tmp = arr[i];
            }

            return Integer.toString(tmp).length();
        }


        public static void radixSort(int[] arr, int digit){

            Vector<Vector<Integer>> contain = new Vector<Vector<Integer>>();

            for(int i=0; i<10; i++){

                Vector<Integer> vettor = new Vector<Integer>();

                contain.add(vettor);
            }

            for(int num:arr){

                int tmp = findDigit(num,digit);

                contain.get(tmp).add(num);
            }

            int p=0;

            for(Vector<Integer> numLink:contain){

                if(numLink.size()>0){

                    for(Integer num:numLink){

                        arr[p++] = num;
                    }
                }
            }

            contain=null;

        }


        public static int findDigit(int num, int digit){

            String numStr = Integer.toString(num);

            if(numStr.length()<digit) return 0;

            return Character.getNumericValue(Character.codePointAt(numStr,numStr.length()-digit));
        }

    }



