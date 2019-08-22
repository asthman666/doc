    namespace System.Linq
    {
        // 抽象类
        internal abstract class EnumerableSorter<TElement>
        {
            // 抽象方法
            internal abstract void ComputeKeys(TElement[] elements, int count);

            // 抽象方法
            internal abstract int CompareKeys(int index1, int index2);

            internal int[] Sort(TElement[] elements, int count)
            {
                this.ComputeKeys(elements, count);
                int[] map = new int[count];
                for (int index = 0; index < count; ++index)
                    map[index] = index;
                this.QuickSort(map, 0, count - 1);
                return map;
            }

            private void QuickSort(int[] map, int left, int right)
            {
                do
                {
                int left1 = left;
                int right1 = right;
                int index1 = map[left1 + (right1 - left1 >> 1)];
                while (true)
                {
                    do
                    {
                        if (left1 >= map.Length || this.CompareKeys(index1, map[left1]) <= 0)
                        {
                        while (right1 >= 0 && this.CompareKeys(index1, map[right1]) < 0)
                            --right1;
                        if (left1 <= right1)
                        {
                            if (left1 < right1)
                            {
                            int num = map[left1];
                            map[left1] = map[right1];
                            map[right1] = num;
                            }
                            ++left1;
                            --right1;
                        }
                        else
                            break;
                        }
                        else
                        goto label_1;
                    }
                    while (left1 <= right1);
                    break;
            label_1:
                    ++left1;
                    }
                    if (right1 - left <= right - left1)
                    {
                    if (left < right1)
                        this.QuickSort(map, left, right1);
                    left = left1;
                    }
                    else
                    {
                    if (left1 < right)
                        this.QuickSort(map, left1, right);
                    right = right1;
                    }
                }
                while (left < right);
            }
        }
    }

    // Assembly location: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\System.Core.dll

    using System.Collections.Generic;

    namespace System.Linq
    {
        internal class EnumerableSorter<TElement, TKey> : EnumerableSorter<TElement>
        {
            internal Func<TElement, TKey> keySelector;
            internal IComparer<TKey> comparer;
            internal bool descending;
            internal EnumerableSorter<TElement> next;
            internal TKey[] keys;

            internal EnumerableSorter(
            Func<TElement, TKey> keySelector,
            IComparer<TKey> comparer,
            bool descending,
            EnumerableSorter<TElement> next)
            {
                this.keySelector = keySelector;
                this.comparer = comparer;
                this.descending = descending;
                this.next = next;
            }

            internal override void ComputeKeys(TElement[] elements, int count)
            {
                this.keys = new TKey[count];
                for (int index = 0; index < count; ++index)
                    this.keys[index] = this.keySelector(elements[index]);
                if (this.next == null)
                    return;
                this.next.ComputeKeys(elements, count);
            }

            internal override int CompareKeys(int index1, int index2)
            {
                int num = this.comparer.Compare(this.keys[index1], this.keys[index2]);
                if (num == 0)
                {
                    if (this.next == null)
                    return index1 - index2;
                    return this.next.CompareKeys(index1, index2);
                }
                if (!this.descending)
                    return num;
                return -num;
            }
        }
    }
