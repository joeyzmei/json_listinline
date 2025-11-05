
Modify the _iterencode_list() function in encode.py so that a list without nesting can be outputted in a single line

Original encode.py line 288-295:

        if _indent is not None:
            _current_indent_level += 1
            newline_indent = '\n' + _indent * _current_indent_level
            separator = _item_separator + newline_indent
            buf += newline_indent
        else:
            newline_indent = None
            separator = _item_separator

The tweak:
```python
	_one_dimension = not any(isinstance(i, (list, tuple, dict)) for i in lst)
        # If it's 1D, format on one line even with indent
        if _one_dimension or _indent is None:
            separator = _item_separator
            newline_indent = None
        else:
            # Multi-dimensional: use original multi-line formatting
            _current_indent_level += 1
            newline_indent = '\n' + _indent * _current_indent_level
            separator = _item_separator + newline_indent
            buf += newline_indent