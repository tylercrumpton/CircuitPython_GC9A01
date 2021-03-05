Introduction
============



.. image:: https://img.shields.io/discord/327254708534116352.svg
    :target: https://adafru.it/discord
    :alt: Discord


.. image:: https://github.com/tylercrumpton/CircuitPython_GC9A01/workflows/Build%20CI/badge.svg
    :target: https://github.com/tylercrumpton/CircuitPython_GC9A01/actions
    :alt: Build Status


.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/psf/black
    :alt: Code Style: Black

displayio driver for GC9A01 TFT LCD displays


Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython <https://github.com/adafruit/circuitpython>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://circuitpython.org/libraries>`_
or individual libraries can be installed using
`circup <https://github.com/adafruit/circup>`_.

Usage Example
=============

.. code-block:: python

    import board
    import displayio
    from gc9a01 import GC9A01

    spi = board.SPI()
    while not spi.try_lock():
        pass
    spi.configure(baudrate=24000000) # Configure SPI for 24MHz
    spi.unlock()
    cs = board.D5
    dc = board.D6
    reset = board.D9

    displayio.release_displays()
    display_bus = displayio.FourWire(spi, command=dc, chip_select=cs, reset=reset)

    display = GC9A01(display_bus, width=240, height=240)

    # Make the display context
    splash = displayio.Group(max_size=10)
    display.show(splash)

    color_bitmap = displayio.Bitmap(240, 240, 1)
    color_palette = displayio.Palette(1)
    color_palette[0] = 0x03C2FC

    bg_sprite = displayio.TileGrid(color_bitmap, pixel_shader=color_palette, x=0, y=0)
    splash.append(bg_sprite)

    while True:
        pass

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/tylercrumpton/CircuitPython_GC9A01/blob/main/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.

Documentation
=============

For information on building library documentation, please check out
`this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.
