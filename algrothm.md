## remove
'
templaate<class _Ty,_Ty _Val>
struct integral_constant{
    static constexpr _Ty value = _Val;
    typedef _Ty value_type;
    typedef integral_constant<_Ty, _Val> type;
    constexpr operator value_type() const noexcept
    {
        return (value);
    }
    constexpr value_type operator()() const noexcept
    {
        return (value);
    }

    typedef integral_constant<bool, true> true_type;
    typedef integral_constant<bool, false> false_type;


}
'

_FwdIt remove(_FwdIt _First, _FwdIt _Last, const _Ty& _Val)

    _First = _Find_unchecked(_First, _Last, _Val) // 找到第一个等于_Val 的迭代器位置

    ：
        	_FwdIt _Next = _First;             //赋值找到第一个的位置
	if (_First != _Last)
		{
		for (++_First; _First != _Last; ++_First)         //从找到的位置开始,位置+1
			if (!(*_First == _Val))                         //如果增后的位置值不等于_Val
				*_Next++ = _STD move(*_First);             // 使用move()将当前位置值向前移,并使_Next位置后移1,
		}
        //循环结束 时，所有不等_Val被移到前面。
	return (_Next);
    其中_Next用于记录位置（不等于_Val的值将移入此，并使其+1）


## unique
'
template<class _FwdIt> inline
	_FwdIt unique(_FwdIt _First, _FwdIt _Last)
	{	// remove each matching previous
	return (_STD unique(_First, _Last, equal_to<>()));
	}

'
'
template<class _FwdIt,
	class _Pr> inline
	_FwdIt unique(_FwdIt _First, _FwdIt _Last, _Pr _Pred)
	{	// remove each satisfying _Pred with previous

	if (_First != _Last)
		for (_FwdIt _Firstb; (void)(_Firstb = _First), ++_First != _Last; ) //创建_Firstb ,使_Firstb为_First，_First+1
			if (_Pred(*_Firstb, *_First))                                   //判断为真（找到第一个连续相同数值位置）
				{	// copy down
				for (; ++_First != _Last; )                                 // _Firstb为重复元素的首次出现位置，_First向后增加，
					if (!_Pred(*_Firstb, *_First))                          //找到不同的元素，则将不同的元素通过move()移动到_Firstb+1的位置，
						*++_Firstb = _STD move(*_First);                    //并且_Firstb改为该元素的位置（即_Firstb+1）,重复逻辑
				return (++_Firstb);                                         //最后返回Firstb+1位置 ，对于排序好的容器保证值唯一。
				}

	return (_Last);
    }
'