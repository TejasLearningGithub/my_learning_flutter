import 'dart:convert';
import 'dart:developer';

import 'package:http/http.dart' as http;

class AddLeadRepo {
  var token =
      'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYzYjQwNzczOWQ2ZWZkNmYxOWNmMDcxNiIsIm5hbWUiOiJzeXN0ZW0gYWRtaW4iLCJlbWFpbCI6InN5c2FkbWluQHN5c3RlbS5jb20iLCJpYXQiOjE2Nzk1NTUzMTcsImV4cCI6MTY4NzMzMTMxN30.xlmKsJlW04AGxwKhZNjVr_M8357M-NbaDr2WYsEhId4';
  //Map<String, dynamic> data = {};
  Future addLeadApi({required Map<String, dynamic> data}) async {
    try {
      var response = await http.post(
          Uri.parse('http://45.79.123.102:49005/api/leads/add'),
          headers: {'Authorization': token},
          body: data);

      if (response.statusCode == 200) {
        log('Response Successful');
      } else {
        log('Error in response');
      }
    } catch (e) {
      log(e.toString());
    }
  }

  Future centerApi() async {
    try {
      var response = await http.get(
          Uri.parse('http://45.79.123.102:49005/api/center/all'),
          headers: {
            'Content-Type': 'application/json',
            'Authorization': token,
          });
      if (response.statusCode == 200) {
        log('Response centerApi Successful');
        return json.decode(response.body);
      } else {
        log('Error in response');
      }
    } catch (e) {
      log('Error = ${e.toString()}');
    }
  }

  Future countryApi() async {
    try {
      var response = await http.get(
          Uri.parse('http://45.79.123.102:49005/api/country/all'),
          headers: {
            'Content-Type': 'application/json',
            'Authorization': token,
          });

      if (response.statusCode == 200) {
        return json.decode(response.body);
      }
    } catch (e) {
      log('Error in country api = ${e.toString()}');
    }
  }

  Future sourceApi() async {
    try {
      var response = await http.get(
          Uri.parse('http://45.79.123.102:49005/api/leads/source'),
          headers: {'Authoriation': token});

      if (response.statusCode == 200) {
        return json.decode(response.body);
      }
    } catch (e) {
      log('Error in accessing source Apis == ${e.toString()}');
    }
  }

  Future cityApi({required int stateId}) async {
    try {
      http.Request request = http.Request(
        'GET',
        Uri.parse('http://45.79.123.102:49005/api/city/getcitybystate'),
      );
      var headers = {'Authorizatipon': token};
      var body = {'state_id': stateId};
      request.headers.addAll(headers);
      request.body = jsonEncode(body);

      http.StreamedResponse response = await request.send();

      if (response.statusCode == 200) {
        String responseBody = await response.stream.bytesToString();
        return json.decode(responseBody);
      }
    } catch (e) {
      log('Error in accessing city api = ${e.toString()}');
    }
  }

  Future programCategoryApi({required String centerId}) async {
    try {
      http.Request request = http.Request(
          'GET',
          Uri.parse(
              'http://45.79.123.102:49005/api/programcategory/getbycenter'));
      var headers = {'Authorizaion': token};
      var body = {'center_id': centerId};
      request.headers.addAll(headers);
      request.body = jsonEncode(body);

      http.StreamedResponse response = await request.send();

      if (response.statusCode == 200) {
        String responseBody = await response.stream.bytesToString();
        return json.decode(responseBody);
      }
    } catch (e) {
      log('Error in accessing program category = ${e.toString()}');
    }
  }

  Future programApi({required String catId}) async {
    try {
      http.Request request = http.Request('GET',
          Uri.parse('http://45.79.123.102:49005/api/program/getbycategory'));
      var headers = {
        'Content-Type': 'application/json',
        'Authorization': token,
      };
      var body = {'cat_id': catId};
      request.headers.addAll(headers);
      request.body = jsonEncode(body);

      http.StreamedResponse response = await request.send();
      if (response.statusCode == 200) {
        String responseBody = await response.stream.bytesToString();
        log('Success');

        return json.decode(responseBody);
      }
    } catch (e) {
      log('Error in program API = ${e.toString()}');
    }
  }

  Future getStateByCountryId({required int countryId}) async {
    try {
      http.Request request = http.Request(
        'GET',
        Uri.parse('http://45.79.123.102:49005/api/state/getstatebycountry'),
      );
      var headers = {
        'Content-Type': 'application/json',
        'Authorization': token,
      };

      var body = {'country_id': countryId};

      request.headers.addAll(headers);
      request.body = jsonEncode(body);

      http.StreamedResponse response = await request.send();

      if (response.statusCode == 200) {
        String responseBody = await response.stream.bytesToString();
        return json.decode(responseBody);
      }
    } catch (e) {
      log('Error in Getting response from state by country = ${e.toString}');
    }
  }

  Future getCityByState({required int stateId}) async {
    try {
      http.Request request = http.Request(
        'GET',
        Uri.parse('http://45.79.123.102:49005/api/city/getcitybystate'),
      );
      var headers = {
        'Content-Type': 'application/json',
        'Authorization': token,
      };
      var body = {'state_id': stateId};

      request.headers.addAll(headers);
      request.body = jsonEncode(body);

      http.StreamedResponse response = await request.send();
      if (response.statusCode == 200) {
        String responseBody = await response.stream.bytesToString();
        log('success');
        return json.decode(responseBody);
      }
    } catch (e) {
      log('Error in repository = ${e.toString()}');
    }
  }

  Future getAllActionPlanned({required String statusId}) async {
    try {
      http.Request request = http.Request(
        'GET',
        Uri.parse('http://45.79.123.102:49005/api/leads/actionplanned'),
      );
      var headers = {
        'Conent-Type': 'application/json',
        'Authorization': token,
      };
      var body = {'status_id': statusId};
      request.headers.addAll(headers);
      request.body = jsonEncode(body);

      http.StreamedResponse response = await request.send();

      if (response.statusCode == 200) {
        String responseBody = await response.stream.bytesToString();
        log('success');
        return json.decode(responseBody);
      }
    } catch (e) {
      log('Error in Action Planned ${e.toString()}');
    }
  }
}
