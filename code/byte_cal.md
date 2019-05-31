# byte 运算的注意事项
## 例子一
```
    public void test{
        int a = 255;
        byte[] bytes = toBytes(a);
        // 不相等，符号位问题
        assert a == byte[1];
    }
    
    public static byte[] toBytes(int val) {
        //int 占用4个字节
        byte[] b = new byte[4];
        for (int i = 3; i > 0; i--) {
            //int 强转byte，丢失高位
            b[i] = (byte) val;
            //无符号右移，无论正负，高位都以0填充
            val >>>= 8;
        }
        b[0] = (byte) val;
        return b;
    }
```
## 例子二
```
    byte[] a = new byte[10];
    a[0]= -127;
    
    int c = a[0]&0xff;
    // 不相等，补码补位置问题
    assert c == a[0];
    
```