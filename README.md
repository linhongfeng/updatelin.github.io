# 自定义View
## 一 自定义View基础

###1,MotionEvent中 get和getRaw的区别
	event.getX();       //触摸点相对于其所在组件坐标系的坐标
	event.getRawX();    //触摸点相对于屏幕默认坐标系的坐标


###2,自定义view,主要分为两类
	
1. 继承自View		-->没有现成的view,需要自己实现
2. 继承自ViewGroup	-->利用现有组件来组成新的组件

###3,测量View大小(onMeasure)
-- 
**View的大小不仅由自身所决定,同时也会受到父控件的影响,为了我们的控件能更好的适应各种情况,一般会自己进行测量.**

    @Override
	protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
		int widthsize = MeasureSpec.getSize(widthMeasureSpec);      //取出宽度的确切数值
		int widthmode = MeasureSpec.getMode(widthMeasureSpec);      //取出宽度的测量模式

    	int heightsize = MeasureSpec.getSize(heightMeasureSpec);    //取出高度的确切数值
    	int heightmode = MeasureSpec.getMode(heightMeasureSpec);    //取出高度的测量模式
	}
- 如果对View的宽高进行修改,不要调用 super.onMeasure(widthMeasureSpec, heightMeasureSpec);要调用setMeasureDimension(widthsize, heightsize);

###4,确定View的大小,在视图大小发生改变的时候调用
	View的大小不仅由View来控制,同事受父控件的影响,所以我们再确定View大小的时候最好使用系统提供的onSizeChange()回调函数

###5,确定子View布局位置(onLayout)
	用于确定子View的位置,在自定义ViewGroup中会用到,他调用的是子View的layout函数.
	在自定义的ViewGroup中,onLayout一般是循环去除子view,然后经过计算得出各个子View位置的坐标值,然后用child.layout(l, t, r, b);来设置子View的位置.

## 二 CanVas之绘制图形
