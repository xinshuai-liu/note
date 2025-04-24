apt-get install  python2-dev autotools-dev libicu-dev build-essential libbz2-dev libboost-all-dev


tar zxvf boost_1_82_0.tar.gz
cd ./boost_1_82_0
./bootstrap.sh --prefix=/usr/
./b2 install

vim ./boosthello.cpp


#include <iostream>
#include <boost/version.hpp>
using namespace std;
int main() {
    cout << "Boost 版本" << BOOST_VERSION << endl;
    return 0;
}

g++ -o boosthello ./boosthello.cpp