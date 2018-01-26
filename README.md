# pytest
examples of python that wrapped by c/c++

#include<python2.7/Python.h>
/* objToJSON */
PyObject* pytest(PyObject* self, PyObject *args, PyObject *kwargs)
{
    (void)args;
    (void)kwargs;
    printf("hello pytest.\n");

    Py_RETURN_NONE;
}
static PyMethodDef pytestMethod[] = {
    {"pytest", (PyCFunction) pytest, METH_VARARGS | METH_KEYWORDS, "this is a py test."},
    {NULL,NULL,0,NULL}
};

PyMODINIT_FUNC initpytest(void)
{
    PyObject *module;
    PyObject *version_string;

    module = Py_InitModule("pytest", pytestMethod);

    if (module == NULL)
    {
        return;
    }

    version_string = PyString_FromString ("version-1.0");
    PyModule_AddObject(module, "__version__", version_string);
}

try:
  from setuptools import setup, Extension
except ImportError:
  from distutils.core import setup, Extension
import distutils.sysconfig
from distutils.sysconfig import customize_compiler
from distutils.command.build_clib import build_clib
from distutils.command.build_ext import build_ext
import os.path
import re
import sys
from glob import glob

CLASSIFIERS = filter(None, map(str.strip,
"""
Development Status :: 5 - Production/Stable
Intended Audience :: Developers
License :: OSI Approved :: BSD License
Programming Language :: C
Programming Language :: Python :: 2.6
Programming Language :: Python :: 2.7
Programming Language :: Python :: 3
Programming Language :: Python :: 3.2
Programming Language :: Python :: 3.4
""".splitlines()))

module1 = Extension(
    'pytest',
     sources = [
         './pytest.c'
     ],
     include_dirs = ['.'],
     extra_compile_args = ['-D_GNU_SOURCE'],
     extra_link_args = ['-lstdc++', '-lm']
)

def get_version():
    return "1.0"

setup(
    name = 'pytest',
    version = get_version(),
    description = "pytest, this is a test.",
    long_description = "description...",
    libraries = [],
    ext_modules = [module1],
    author="wzugang",
    author_email="1098501555@qq.com",
    download_url="",
    license="GPL License",
    platforms=['any'],
    url="http://wangzugang.net",
    cmdclass = {'build_ext': build_ext},
    classifiers=CLASSIFIERS,
)
