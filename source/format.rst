.. _format:

===============
Format Text
===============


Escape Characters
===========================

Escape the opening and closing brackets.

Press \<return\> for continue
Use inline literal markup.

Press ``<return>`` for continue
Use semantic markup with the kbd role:

Press :kbd:`<return>` for continue
IMO, the last option is the most appropriate for this situation. The first option is the least appropriate.



Marker
===========================
This is a normal text paragraph. The next paragraph is a code sample::

   It is not processed in any way, except
   that the indentation is removed.

   It can span multiple lines.

This is a normal text paragraph again.


Bold
===========================
**text 1a**

:strong:`text 1b`

Italic
===========================
*text 2a*

:emphasis:`text 2b`

Literal
===========================
``text 3a``
:literal:`text 3b`

Match
===========================
The input format is LaTeX math syntax without the “math delimiters“ ($ $), for example:

The area of a circle is :math:`A_\text{c} = (\pi/4) d^2`.

See the `\"math\" directive <https://docutils.sourceforge.io/docs/ref/rst/directives.html#math>`_ (producing display formulas) for more info on mathematical notation in reStructuredText.


Hyperlinks
===========================

**External links**
Use `Sphinx guideline <http://sphinx-doc.org/en/master/usage/restructuredtext/index.html>`_ for inline web links. If the link text should be the web address, you don’t need special markup at all, the parser finds links and mail addresses in ordinary text.

Important
There must be a space between the link text and the opening < for the URL.

This is a paragraph that contains `a link`_.

.. _a link: https://domain.invalid/


Tables
===========================
+------------------------+------------+----------+----------+
| Header row, column 1   | Header 2   | Header 3 | Header 4 |
| (header rows optional) |            |          |          |
+========================+============+==========+==========+
| body row 1, column 1   | column 2   | column 3 | column 4 |
+------------------------+------------+----------+----------+
| body row 2             | ...        | ...      |          |
+------------------------+------------+----------+----------+


====================  =====   ========
A                     B       A and B
====================  =====   ========
False                 False   False
True                  False   False
False                 True    False
True                  True    True
====================  =====   ========


Subscript and Superscript
===========================

Whitespace or punctuation is required around interpreted text, but often not desired with subscripts & superscripts. Backslash-escaped whitespace can be used; the whitespace will be removed from the processed document:

H\ :sub:`2`\ O

E = mc\ :sup:`2`

(a + b)\ :sup:`2` = a\ :sup:`2` + b\ :sup:`2` + 2ab

In such cases, readability of the plain text can be greatly improved with substitutions [2]:

The chemical formula for pure water is |H2O|.

.. |H2O| replace:: H\ :sub:`2`\ O


Code
===========================

Method 1: code-block
--------------------------------

.. code-block:: python

   def hello():
       print("Hello, Sphinx!")


.. code-block:: c

   #include <stdio.h>

   int main() {
       printf("Hello world!\n");
       return 0;
   }

Method 2: use \:\:
--------------------------------

Đây là một đoạn code::

   print("Hello, world!")


Method 3: use directive literalinclude
--------------------------------------

Chèn file code từ bên ngoài::

    ..literalinclude:: my_script.py
        :language: python
        :linenos:

Ưu điểm: Không cần sao chép mã vào tài liệu, dễ bảo trì.


Method 4: parsed-literal
--------------------------------

.. parsed-literal::

   Đây là một biến: ``my_variable``

Method 5: inline code
--------------------------------

Hiển thị code inline. Nếu bạn chỉ cần một đoạn code ngắn trong dòng văn bản, hãy dùng dấu \`\`

Bạn có thể dùng ``print("Hello")`` trong Python.


Cross Reference
===========================

If you place a label directly before a section title, you can reference to it with \:ref\:\`label-name\`. For example::

    .. _my-reference-label:
    Section to cross-reference
    --------------------------
    This is the text of the section.
    It refers to the section itself, see :ref:`my-reference-label`.


Field Column List
===========================

:fieldname: Field content
:param my_arg: The first of my arguments.
:param my_other_arg: The second of my arguments.
:returns: A message (just for me, of course).


Note, Warning
===========================

Màu của khung::

    note: màu lam
    caution: màu cam
    danger: cam đậm

.. warning::

   Hãy cẩn thận khi thay đổi cấu hình hệ thống!
   
   - Hãy sao lưu dữ liệu trước khi thực hiện.
   - Kiểm tra quyền truy cập của bạn.


.. important::

   Đây là lưu ý quan trọng trước khi làm việc!


Image (Hình ảnh)
===========================

.. image:: images/gnu.png
.. figure:: images/gnu.*


Footnotes
===========================

Nội dung ý về ROCE\ [#f1]_ và DMA\ [#f2]_ xem bên dưới

Footnote sẽ được chèn ở cuối trang.


.. rubric:: Footnotes

.. [#f1] RMDA trên nền Ethernet.
.. [#f2] Thực hiện truy cập bộ nhớ không cần CPU.


Comments
===========================

``.. This is a comment.``

You can indent text after a comment start to form multiline comments::

    ..
        This whole indented block
        is a comment.
        Still in the comment.


