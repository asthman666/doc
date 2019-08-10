抽象属性

    public abstract class BaseForm 
    {
        public abstract string PageName { get; }
    }

    // 抽象类不需要实现 BaseForm 的抽象属性    
    public abstract class DataForm : BaseForm 
    {

    }

    // 非抽象类必须实现 BaseForm 的抽象属性
    public class CustomerPage : DataForm 
    {
        public override string PageName
        {
            get { return "License Report Submission"; }
        }    
    }