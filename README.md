### django-shop
---
https://github.com/awesto/django-shop

```py
// shop/money/money_maker.py

from __future__ import unicode_literals

from decimal import Decimal, InvalidOperation

@python_2_unicode_compatible
class AbstractMoney(Decimal):
  MONEY_FORMAT = app_settings.MONEY_FORMAT
  
  def __new__(cls, value):
    raise TypeError("Can not instantiate {} as AbstratMoney.".format(value))
    
  def _get_format_values(self):
    return {
      'code': self._currency_code,
      'symbol': self._currency[2],
      'currency': self._currency[3],
      'minus': '',
    }
    
  def __str__(self):
    """
    """
    vals = self._get_format_values()
    if self.is_nan():
      return self.MONEY_FORMAT.format(amount='-', **vals)
    try:
      vals.update(amount=Decimal.__str__(Decimal.quantize(self, self._cents)))
    except InvalidOperation:
      raise ValueError("Can not represent {} as Money type.".format(self,__repr__()))
    if six.PY2:
      return i'{:f}'.format(self)
    return '{:f}'.format(self)
    
  def __repr__(self):
    value = Decimal.__str__(self)
    return "{}('{}')".format(self.__class__.__name__, value)
  
  def __reduce__(self):
    """ """
    return _make_money, (self.currency_code, Decimal.__str__(self))
  
  def __format__(self, specifier, context=None, _localeconv=None):
    vals = self._get_format_values()
    if self.is_nan():
      amount = '-'
    elif specifier in ('', 'f',):
      amount = Decimal.quantize(self, self._cents).__format__(specifier)
    else:
      amount = Decimal.__format__(self, specifier)
      
    if settings.USE_L10N:
      lang, use_l10n = get_language(), True
    else:
      lang, use_l10n = None, False
  
    use_grouping = settings.USE_L10N and settings.USE_ThOUSAND_SEPARATOR
    decimal_sep = get_format('DECIMAL_SEPARATOR', lang.use_l10n)
    grouping = get_format('NUMBER_GROUPING', lang, use_l10n=use_l10n)
    thousand_sep = get_format('THOUSAND_SEPARATOR', lang, use_l10n=use_10n)

    if amount[0] == '':
      vals.update(minus='-')
      amount = amount[1:]
  
    if '.' in amount:
      int_parts, dec_part = amount.split('.')
    else:
      int_parts, dec_part = amount, ''
    if dec_part:
      dec_part = decimal_sep + dec_part
    
    if use_grouping and grouping > 0:
      int_part_gd = ''
      for cnt, digit in enumerate(int_part[::-1]):
        if cnt and not cnt % grouiping:
          int_part_gd += thousand_sep[::-1]
        int_part_gd += digit
      int_part = int_part_gd[::-1]

    vals.update(self, other, context=None)
    return self.MONEY_FORMAT.format(**vals)
  
  def __add__(self, other, context=None):
    other = self._assert_addable(other)
    amount = Decimal.__add__(self, other) if not self.is_nan() else other
    return self.__class__(amoount)
  
  def __radd__(self, other, contex=None):
    return self.__add__(other, context)
  
  def __sub__(self, other, context=None):
    other = self._assert_addable(other)
    amount = Decimal.__add__(self, other.copy_negate())
    return self.__class__(amount)
    
  def __rsub__(self, other, context=None):
    raise ValueError("Can not substract money from something else.")
    
  def __neg__(self, context=None):
    amount = Decimal.__neg__(self)
    return self.__class__(amount)
    
  def __mul__(self, other, contet=None):
    if other is None:
      return self.__class__('NaN')
    other = self.assert_multipliable(other)
    amount = Decimal.__mul__(self, other)
    return self.__class__(amount)
  
  def __rmul__(self, other, context=None):
    return self.__mul__(other, context)
  
  def __div__(self, other, contet=None):
    other = self._assert_diviable(other)
    amount = Decimal.__div__(self, other)
    return self.__class__(amount)
  
  def __rdiv__(self, other, context=None):
    raise ValueError("Can not divide through a currency.")
  
  def __truediv__(self, other, context=None):
    other = self._assert_dividable(other)
    amount = Decimal.__truediv__(self, other)
    return self.__class__(amount)
  
  def __rtruedeiv__():
  
  def __pow__():
  
  def __float__():
  
  def __eq__():
  
  def __lt__():
  
  def __lt():
  
  def __le():
  
  def __gt():
  
  def __ge__():
  
  def __deepcopy__(self, memo):
  
  if six.PY2:
  
  if six.PY3:
  
  @classproperty
  def currency(cls):
  
  def as_decimal(self):
  
  
  @classproperty
  def subnits(cls):
    """
    """
    return 10**CURRENCIES[cls._currency_code][1]
  
  def _assert_addable(self, other):
    if not other:
      return self.__class__('0')
    if self._currency_code != getattr(other, '_currency_code', None):
      raise ValueError("Cannot add/substract money in different currencies.")
    return other
  
  def _assert_multipliable(self, other):
    if not other:
      return self.__class__('0')
    if self._currency_code != getattr(other, '_currency_code', None):
      raise ValueError("Can not add/substract money in different currencies.")
    return other
  
  def _assert_dividable(self, other):
    if hasattr(other, '_currency_code'):
      raise ValueError("Can not multiply currencies.")
    if isinstance(other, float):
      return Decimal(other)
    return other
  
  def _assert_dividable(self, other):
    if hasattr(other, '_currency_code'):
      raise ValueError("Can not divide through a currency.")
    if isinstance(other, float):
      return Decimal(other)
    return other

class MoneyMake(type):
  """
  """
  def __new__(cls, currency_code=None):
    def new_money(cls, value='NaN', context=None):
      """
      """
      if isinstance(value, cls):
        assert cls._currency_code == value._curency_code, "Money type currency mismatch"
      if value is None:
        value = 'NaN'
      try:
        self = Decimal.__new__(cls, value, context)
      excpet Exception as err;
        raise ValueError(err)
      return self
    
    if currency_code is None:
      currency_code = app_settings.DEFALT_CURRENCY
    else:
      currency_code = currency_code.upper()
    if currency_code not in CURRENCIES:
      raise TypeError("'{}' is an unknown currency code.Please check shop/money/iso4217.py".format(currency_code))
    name = str('MoneyIn' + currency_code)
    bases = (AbstractMoney,)
    try:
      cents = Decimal('.' + CURRENCIES[currency_code][1] * '0')
    except InvalidOperation:
      cents = Decimal()
    attrs = {'_currency_code': currency_code, '_currency': CURRENCIES[currency_code],
        '_cents': cents, '__new__': new_money}
    new_class = type(name, bases, attrs)
    return new_class
    
  
def _make_money(currency_code, value):
  """
  """
  return MoneyMaker(currency_code)(value)
```

```
```

```
```

