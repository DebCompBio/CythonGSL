CythonGSL
*********

CythonGSL provides a set of Cython declarations for the GNU Scientific Library (GSL).

Cython is the ideal tool to speed up numerical computations. While SciPy provides many numerical tools such as optimizers and integrators they still are not as fast as they could be because of the Python function call overhead (even if your evaluation function is written cython). CythonGSL allows you to shave off that last layer by calling directly into the c functions from your Cython code.

Fork of PyrexGsl by Mario Pernici (http://wwwteor.mi.infn.it/~pernici/pyrexgsl/pyrexgsl.html).

Dependencies
************

* Python
* Cython
* GSL (for a windows port see http://gnuwin32.sourceforge.net/packages/gsl.htm)

Installation
************

Execute setup.py which will tell you how to install cython_gsl in the correct way. Make sure to include the --install-lib flag when installing.

Usage
*****

In your cython file from which you want to call gsl routines, import gsl:
>>> from cython_gsl cimport *

From there you should be able to call any gsl function, see http://www.gnu.org/software/gsl/manual/gsl-ref.html for the GSL reference.

Compilation
***********

I haven't quite figured out the best way to find the gsl directories in the setup.py file under windows, any suggestions are welcome.

Here is what a setup.py could look like:

::

    from distutils.core import setup
    from distutils.extension import Extension
    from Cython.Distutils import build_ext
    import numpy as np
    import cython_gsl

    setup(
        [...]
        include_dirs = [np.get_include(), cython_gsl.get_include()],
        cmdclass = {'build_ext': build_ext},
        ext_modules = [Extension("my_cython_script", ["src/my_cython_script.pyx"], libraries=['gsl','gslcblas'], library_dirs=cython_gsl.get_library_dir())]
        )

