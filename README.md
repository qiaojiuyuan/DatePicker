# DatePicker
# 选择时间控件
## 原作者git链接 https://github.com/liuwan1992/CustomDatePicker

```
我是基于原作者的代码基础上做了一些优化，如选择年份或其它时间之后不会初始化其它已经选好的时间。
具体下载下原作者的对比就知道了，文字不太好描述清楚。
还有一些我们项目中需求的一些小细节功能点。
感谢原作者提供的源码让我减少了很多开发时间，因为我们领导说做这个控件加上内部我们自己的逻辑只能给我3小时...
我当时内心是崩溃的，为什么领导总感觉这些东西很好做的样子...
修改代码逻辑的期间还遇到一个坑，就是有的月份有31日有的月份没有，当从有31日的切换到无31日的月份时，再从selectedCalender取
月份时会被自动加1，从而取得的当前月的日期数不准，所以要先还原为1日，然后再设置月份，再取日期数。这块代码我做了注释。
```
```java
        month_pv.setOnSelectListener(new DatePickerView.onSelectListener() {
            @Override
            public void onSelect(String text) {
                int currentDay = selectedCalender.get(Calendar.DAY_OF_MONTH);
                //因为有的月份有31日有的月份没有，当从有31日的切换到无31日的月份时，再从selectedCalender取
                //月份时会被自动加1，从而取得的当前月的日期数不准，所以要先还原为1日，然后再设置月份，再取日期数
                selectedCalender.set(Calendar.DAY_OF_MONTH, 1);
                selectedCalender.set(Calendar.MONTH, (Integer.parseInt(text) - 1));
                int newDay = selectedCalender.getActualMaximum(Calendar.DAY_OF_MONTH);
                if (currentDay > newDay) {
                    selectedCalender.set(Calendar.DAY_OF_MONTH, newDay);
                } else {
                    selectedCalender.set(Calendar.DAY_OF_MONTH, currentDay);
                }
                dayChange();
            }
        });
```
![项目图](https://github.com/qiaojiuyuan/DatePicker/raw//master/img/datePicker_1.png)
![项目图](https://github.com/qiaojiuyuan/DatePicker/raw//master/img/datePicker_2.png)
![项目图](https://github.com/qiaojiuyuan/DatePicker/raw//master/img/datePicker_3.png)
