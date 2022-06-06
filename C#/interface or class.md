	// Summary:
	// Exposes an enumerator, which supports a simple iteration over a non-generic collection.
    public interface IEnumerable
	{
		IEnumerator GetEnumerator();
	}

	// Summary:
	//     Exposes the enumerator, which supports a simple iteration over a collection of
	//     a specified type.
	public interface IEnumerable<out T> : IEnumerable
	{
		IEnumerator<T> GetEnumerator();
	}

	// Summary:
	//     Defines methods to manipulate generic collections.
	public interface ICollection<T> : IEnumerable<T>, IEnumerable
	{
		int Count { get; }
		bool IsReadOnly { get; }
		void Add(T item);
		void Clear();
		bool Contains(T item);
		void CopyTo(T[] array, int arrayIndex);
		bool Remove(T item);
	}    

	//
	// Summary:
	//     Represents a collection of objects that can be individually accessed by index.
	public interface IList<T> : ICollection<T>, IEnumerable<T>, IEnumerable
	{
		T this[int index] { get; set; }
		int IndexOf(T item);
		void Insert(int index, T item);
		void RemoveAt(int index);
	}    

	// Summary:
	//     Represents a strongly typed list of objects that can be accessed by index. Provides
	//     methods to search, sort, and manipulate lists.
    public class List<T> : ICollection<T>, IEnumerable<T>, IEnumerable, IList<T>, IReadOnlyCollection<T>, IReadOnlyList<T>, ICollection, IList {        
		public void ForEach(Action<T> action);
		// more ...
    }

[Ilist or list](https://stackoverflow.com/questions/8717582/why-use-ilist-or-list)

<a href="https://stackoverflow.com/questions/1072614/should-i-always-return-ienumerablet-instead-of-ilistt">IEnumerable&lt;T&gt; or IList&lt;T&gt;</a>

