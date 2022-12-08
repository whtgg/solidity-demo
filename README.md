# solidity-demo 学习笔记

```
contract ArrayTy {

    //######ArrayTy######
    // 固定长度 Array
    uint[8] array1;
    bytes1[5] array2;
    address[100] array3;

    // 可变长度 Array
    uint[] array4;
    bytes1[] array5;
    address[] array6;
    bytes array7;

    // 初始化可变长度 Array
    uint[] array8 = new uint[](5);
    bytes array9 = new bytes(9);
    //  给可变长度数组赋值
    function initArray() external pure returns(uint[] memory){
        uint[] memory x = new uint[](3);
        x[0] = 1;
        x[1] = 3;
        x[2] = 4;
        return(x);
    }  
    function arrayPush() public returns(uint[] memory){
        //数组不可以修改
        uint[2] memory a = [uint(1),2];
        array4 = a;
        array4.push(3);
        return array4;
    }

    //#####Struct#######
    struct people {
        string name;
        uint age;
    }
    
    // 结构体初始化并且声明为可见
    people public pl;

    function initial_people() public {
        // 直接修改消耗gas
        pl.name = "jack";
        pl.age = 19;
    }

    function initial_people_x() public view returns(people memory){
        // 做一份拷贝 不消耗gas
        people memory _pl = pl;
        _pl.name = "juse";
        _pl.age = 18;
        return _pl;
    }


    //#####Enum#######
    // 声明类型
    enum ActionSet { Create,Update,Finish}

    // 初始化
    ActionSet create = ActionSet.Update;

    /// 作为参数  enum可以直接转换为uint
    function enum_convert() public view returns(uint) {
        return uint(create);
    }

    //#####Mapping#######
    mapping(string=>address) public map1;
    struct People {
        string name;
        uint  age;
    }
    // Only elementary types, contract types or enums are allowed as mapping keys.
    //mapping(People=>string) public jock;
    /// _key必须添加 memory/calldata  不然报错TypeError: Data location must be "memory" or "calldata" for parameter in function, but none was given
    // 因为string是引用类型 必须指定其localtion
    function change_map(string memory _key,address  _addr) public  {
        map1[_key] = _addr;
    }
}

```