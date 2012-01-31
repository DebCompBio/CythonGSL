CythonGSL
*********

CythonGSL provides a set of Cython declarations for the GNU Scientific Library (GSL).

Cython is the ideal tool to speed up numerical computations by converting typed Python code to C and generating Python wrappers so that these compiled functions can be called from Python. Scientific programming often requires use of various numerical routines (e.g. numerical integration, optimization). While SciPy provides many of those tools, there is an overhead associated with using these functions within your Cython code. CythonGSL allows you to shave off that last layer by providing Cython declarations for the GSL which allow you to use this high-quality library from within Cython without any Python overhead.

Fork of PyrexGsl by Mario Pernici (http://wwwteor.mi.infn.it/~pernici/pyrexgsl/pyrexgsl.html).

Dependencies
************

* Python
* Cython (http://cython.org)
* GSL (for a windows port see http://gnuwin32.sourceforge.net/packages/gsl.htm)

Installation
************

Execute setup.py which will tell you how to install cython_gsl in the correct way. Make sure to include the --install-lib flag when installing.

Usage
*****

In your cython file from which you want to call gsl routines, import gsl like this:

::

    from cython_gsl cimport *

From there you should be able to call any gsl function, see http://www.gnu.org/software/gsl/manual/gsl-ref.html for the GSL reference.

For more examples, check out the examples directory.

Compilation
***********

Here is what your setup.py could look like:

::

    from distutils.core import setup
    from Cython.Distutils import Extension
    from Cython.Distutils import build_ext
    import cython_gsl

    setup(
        [...]
        include_dirs = [cython_gsl.get_include()],
        cmdclass = {'build_ext': build_ext},
        ext_modules = [Extension("my_cython_script", ["src/my_cython_script.pyx"], libraries=['gsl','gslcblas'], library_dirs=cython_gsl.get_library_dir(), cython_include_dirs=cython_gsl.get_cython_include_dir())]
        )

