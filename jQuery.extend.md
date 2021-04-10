[jQuery.extend() | jQuery API Documentation](https://api.jquery.com/jquery.extend/)

```javascript
jQuery.extend = jQuery.fn.extend = function() {
	debugger;
	var src, copyIsArray, copy, name, options, clone,
		target = arguments[0] || {}, // 有沒有參數進來，如果沒有，target = {}
		i = 1,
		length = arguments.length, // 參數長度
		deep = false;

	// Handle a deep copy situation
	if ( typeof target === "boolean" ) { // 第一個參數如果是 TRUE OR FALSE
		deep = target;                   // 如果是 TRUE 將處理 Deep Copy
                                         // 再判斷，有沒有第二個參數進來，
                                         // 如果沒有，target = {}
		// skip the boolean and the target
		target = arguments[ i ] || {};   
		i++;                             
	}

	// Handle case when target is a string or something (possible in deep copy)
	if ( typeof target !== "object" && !jQuery.isFunction(target) ) {
		target = {}; // 如果 target 不是 Object 也不是 Function，target 將改成 {}
	}

	// extend jQuery itself if only one argument is passed
	if ( i === length ) { // 如果只傳入一個參數，而且不是傳入 TRUE OR FALSE
		target = this;    // target 將改成 jQuery
		i--;              // i 減 1，下面的 for 迴圈，至少執行一次
	}

	for ( ; i < length; i++ ) {
		// Only deal with non-null/undefined values
		if ( (options = arguments[ i ]) != null ) {
			// Extend the base object
			for ( name in options ) {
				src = target[ name ];
				copy = options[ name ];

				// Prevent never-ending loop
				if ( target === copy ) {
					continue; // 如果與原本名稱相同，且為同一個物件，則跳過。 (避免重複施作)
				}

				// Recurse if we're merging plain objects or arrays
				if ( deep && copy && ( jQuery.isPlainObject(copy) || (copyIsArray = jQuery.isArray(copy)) ) ) {
					if ( copyIsArray ) {
						copyIsArray = false;
						clone = src && jQuery.isArray(src) ? src : [];

					} else {
						clone = src && jQuery.isPlainObject(src) ? src : {};
					}

					// Never move original objects, clone them
					target[ name ] = jQuery.extend( deep, clone, copy );

				// Don't bring in undefined values
				} else if ( copy !== undefined ) {
					target[ name ] = copy;
				}
			}
		}
	}

	// Return the modified object
	return target;
};
```









