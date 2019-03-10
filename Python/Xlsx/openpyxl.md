#关于openpyxl模块读取xlsx文件中合并模块出错问题

在window环境下，使用openpyxl模块读取xlsx文件的时候，会产生“合并单元没有value成员”的错误：
    
    AttributeError: 'MergedCell' object has no attribute 'value'
但是在Ubuntu系统上，却能正确运行。
通过测试代码：

#!/usr/bin/env python3

    from openpyxl import   load_workbook
    
    wb = load_workbook  ('test.xlsx')
    ws = wb['Sheet1']
    print(ws.max_row)
    print(ws.max_column)
    mc = ws.merged_cells
    print(dir(mc))
    for emc in mc:
        print(emc)
        print(dir(emc))
    print(ws['A1'].value)
    print(ws['A2'].value)
测试发现，在Window中，读取合并单元格的时候，只能通过第一个左上角位置读取，其它位置并不会像Linux系统上读取出None，而会产生异常。
解决的方法是，控制读取操作，对于合并单元格的读取，测试读取是否位于合并单元格内部，如果处于内部，只读取左上角位置，作为整个合并单元格中任意位置的单元格的值。