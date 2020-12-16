# Heap

* **complete** all levels must be filled from left to right.
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-complete-1.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-complete-2.png)

* **incomplete**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-incomplete-1.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-incomplete-2.png)

* **heap property** each node greater than or equal to its childs.
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-property.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-property-invalid.png)

* **bubble up**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-bubble-up.png)

* **bubble down**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-bubble-down.png)

* **complexity**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-insert-complexity.png)

--                 |        indexing     | search              | add                 | remove
-------------------|---------------------|---------------------|---------------------|-----------------------
Heap               | O(log n)            | O(log n)            | O(log n)            | O(log n)


* **array index**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-array-index.png)

* **applications**

  * **heap sort**
    * insert all array elments to a heap
    * remove one by one and put them to the array in order
    * now you have sorted array
    
  * **priority queue**
    * look at PriorityQueue section with Heap
    
  * **heapify** is transform an array to a heap in place.

        public class Main {
            public static void main(String[] args) {
                Integer[] array = {5, 3, 8, 4, 1, 2};
                CustomHeap.heapify(array);
                System.out.println(Arrays.toString(array)); //[8, 4, 5, 3, 1, 2]
            }
        }

        public class CustomHeap {
            public static <T extends Number & Comparable<T>> void heapify(T[] array) {
                int lastParentIndex = array.length / 2 - 1;
                for(int i=lastParentIndex;i>=0;i--) {
                    bubbleDown(array, i);
                }
            }

            private static <T extends Number & Comparable<T>> void bubbleDown(T[] array, int index) {
                while(index < array.length && !isValidParent(array, index)) {
                    swap(array, index, largerChildIndex(array, index));
                    index = largerChildIndex(array, index);
                }
            }

            private static <T extends Number & Comparable<T>> boolean isValidParent(T[] array, int index) {
                if(!hasLeftChild(array, index))
                    return true;

                if(!hasRightChild(array, index))
                    return array[index].compareTo(array[leftIndex(index)]) >= 0;

                return array[index].compareTo(array[leftIndex(index)]) >= 0
                        && array[index].compareTo(array[rightIndex(index)]) >= 0;
            }

            private static <T extends Number & Comparable<T>> void swap(T[] array, int index1, int index2) {
                T temp = array[index1];
                array[index1] = array[index2];
                array[index2] = temp;
            }

            private static <T extends Number & Comparable<T>> int largerChildIndex(T[] array, int index) {
                if(!hasLeftChild(array, index))
                    return index;

                if(!hasRightChild(array, index))
                    return leftIndex(index);

                return (array[leftIndex(index)].compareTo(array[rightIndex(index)]) > 0)
                        ? leftIndex(index) : rightIndex(index);
            }

            private static <T extends Number & Comparable<T>> boolean hasLeftChild(T[] array, int index) {
                return leftIndex(index) < array.length;
            }

            private static <T extends Number & Comparable<T>> boolean hasRightChild(T[] array, int index) {
                return rightIndex(index) < array.length;
            }

            private static int parentIndex(int index) {
                return (index - 1) / 2;
            }

            private static int leftIndex(int index) {
                return 2 * index + 1;
            }

            private static int rightIndex(int index) {
                return 2 * index + 2;
            }
        }

  * **Kth Largest Item**
    * insert all array items in heap
    * then remove (k-1) items from heap
    * the root of heap now is the Kth item
