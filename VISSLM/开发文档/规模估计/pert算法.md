# pert 算法

	平均值 ：   average
	估计结果：  result
	偏差：      deviation
	最大值：    maxValue
	最小值：    minValue


* 估计人数 大于或等于 3   人:
	
		每人输入一个估计值,   average 为所有值求平均
		maxValue 取最大的值,  minValue 取最小的值
		A为最大值，B为最小值，M为剩下的值的平均
		result =((A + 4 × M + B))/6
		deviation=  Max(maxValue - average,average - minValue)/(average )

* 否则：

		每人输入三个估计值 A, M, B
		maxValue 取最大的值,  minValue 取最小的值
		人数 number
		所有人的A值的总和 AT， M值的总和MT， B值的总和 BT
		average =((AT + MT + BT))/(3 × number)
	
		result=((AT/number  + 4 × (MT/number)  + BT/number))/6
	
		deviation=  Max(maxValue - average,average - minValue)/(average )
