---
layout: post
title: jQuery Datepicker 깜빡임 현상 해결하기
date: 2015-06-17 00:00:00
categories: jQuery
---

Datepicker 를 사용하여 선택하는 날짜를 받아오는 이벤트는 onSelect 이다. CSS 요소가 크게 영향이 없는 형태로 사용한다면, 문제가 되지 않는다. 하지만 브라우저에 부담을 주는 요소를 사용하는 경우 깜빡임 현상이 나타 날 수 있다.

최근에 겪은 사례로는 background 요소를 적용 한 경우 발생 했다. setTimeout( fun, 200 ) 을 사용해서 시점을 천천히 하여 보면, 초기화 된 후 재 생성 되는 부분을 확인 할 수 있다. 즉 CSS 는 초기화 된다.

아래 소스는 jquery-ui.js 중 datepicker onSelect 함수를 Callback 하는 부분이다. trigger custom callback 부분을 보도록 한다. 두개 인자를 제공 한다.

- dateStr: 날짜 문자열
- inst: Datepicker Object

```javascript
/* Update the input field with the selected date. */
_selectDate: function(id, dateStr) {
    var onSelect,
        target = $(id),
        inst = this._getInst(target[0]);

    dateStr = (dateStr != null ? dateStr : this._formatDate(inst));
    if (inst.input) {
        inst.input.val(dateStr);
    }
    this._updateAlternate(inst);

    onSelect = this._get(inst, "onSelect");
    if (onSelect) {
        onSelect.apply((inst.input ? inst.input[0] : null), [dateStr, inst]);  // trigger custom callback
    } else if (inst.input) {
        inst.input.trigger("change"); // fire the change event
    }

    if (inst.inline){
        this._updateDatepicker(inst);
    } else {
        this._hideDatepicker();
        this._lastInput = inst.input[0];
        if (typeof(inst.input[0]) !== "object") {
            inst.input.focus(); // restore focus
        }
        this._lastInput = null;
    }
},
```

inst.inline 기준에 따라 this._updateDatepicker( inst ) 함수를 호출 하여 위에서 언급한 상황이 재연 된다. 현상을 해결 하기 위해서는 onSelect 함수를 아래와 같이 구현하여 호출 되지 않도록 해야 한다.

```javascript
$datepicker.datepicker( {
  inline: true,
  showOtherMonths: true,
  showMonthAfterYear: true,
  monthNames: [ '01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12' ],
  dayNamesMin: [ '일', '월', '화', '수', '목', '금', '토' ],

  onSelect: function( date, inst ) {
    inst.inline = false; // datepicker object inline false 변경
    customSelect( date ); // 사용자 정의 구현 함수
  }
} );
```

위 소스를 참고하여 적용 한다면, 깜박임 현상은 해결 된다. customSelect( date ) 로 정의한 함수는 스타일에 맞게 적용 하도록 한다.

참고

- [http://jqueryui.com/download/](http://jqueryui.com/download/)
