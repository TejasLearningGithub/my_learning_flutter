import 'dart:developer';

import 'package:accessing_kido_apis/ADD_LEAD/model/action_planned.dart';
import 'package:accessing_kido_apis/ADD_LEAD/model/center_modal.dart';
import 'package:accessing_kido_apis/ADD_LEAD/model/city.dart';
import 'package:accessing_kido_apis/ADD_LEAD/model/country.dart';
import 'package:accessing_kido_apis/ADD_LEAD/model/programs.dart';
import 'package:accessing_kido_apis/ADD_LEAD/model/state_modal.dart';

import 'package:flutter/material.dart';

import 'add_lead_repo.dart';

enum Gender {
  male,
  female,
}

enum YesNo {
  yes,
  no,
}

class AddLeadProvider with ChangeNotifier {
  AddLeadRepo addLeadRepository = AddLeadRepo();
  List<ActionPlannedModel> listOfActions = [];
  List<Programs> listPrograms = [];
  List<Programs> myTempList = [];
  List<CenterModal> centerList = [];
  List<StateByCountryId> stateList = [];
  // String? authToken;
  List<IndiaCountryModal> countryList = [];
  List<CitiesByState> cityList = [];
  // List<SourceModel> sourceList = [];
  // List<CityModel> cityList = [];
  // List<StateModel> stateList = [];
  // List<ProgramModel> programList = [];
  // List<CenterModel> centerList = [];
  // ProgramCatModel programCatModel = ProgramCatModel(
  //   id: '',
  //   schoolName: '',
  //   schoolDisplayName: '',
  //   programcategoryIdList: [],
  // );

  /// textfield values
  String? childFirstName;
  String? childLastName;
  String? parentName;
  String? parentFirstContact;
  String? parentSecondContact;
  String? parentEmail;
  String? parentEducation;
  String? parentProfession;
  String? secondaryParentName;
  String? secondaryFirstContact;
  String? secondarySecondContact;
  String? secondaryEmail;
  String? secondaryEducation;
  String? secondaryProfession;
  String? parentPinCode;
  String? parentLandmark;
  String? parentHouse;
  String? parentStreet;
  String? parentAddress;
  String? parentArea;
  String? remark;

  bool addingNew = false;

  /// checkbox values
  bool whatsAppFirst = true;
  bool whatsAppSecond = false;
  bool secondaryFirstWhatsApp = true;
  bool secondarySecondWhatsApp = false;
  bool sibling = false;

  /// dropdown values
  String? parentCountry;
  String? parentState;
  String? parentCity;
  String? statusId;
  String? subStatusId;
  String? programCatagoryId;
  String? programId;
  String? schoolId;
  String? sourceCatagory;
  String? primaryParent;
  String? secondaryParentType;

  /// multi selection dropdown lists
  List<String> parentKnowAboutUs = [];
  List<String> actionTaken = [];

  /// radio button values
  Gender childGender = Gender.male;
  YesNo childPreSchool = YesNo.no;

  /// date picker value
  DateTime? childDoB;

  resetScreen() {
    //authToken = null;
    //cityList = [];
    //ountryList = [];
    //  sourceList = [];
    //   cityList = [];
    //   stateList = [];
    //   programList = [];
    //   centerList = [];
    //   programCatModel = ProgramCatModel(
    //     id: '',
    //     schoolName: '',
    //     schoolDisplayName: '',
    //     programcategoryIdList: [],
    //   );
    //   childFirstName = null;
    childLastName = null;
    parentName = null;
    parentFirstContact = null;
    parentSecondContact = null;
    parentEmail = null;
    secondaryParentName = null;
    secondaryFirstContact = null;
    secondarySecondContact = null;
    secondaryEmail = null;
    parentEducation = null;
    parentProfession = null;
    secondaryEducation = null;
    secondaryProfession = null;
    parentPinCode = null;
    parentLandmark = null;
    parentHouse = null;
    parentStreet = null;
    parentAddress = null;
    parentArea = null;
    remark = null;
    whatsAppFirst = true;
    whatsAppSecond = false;
    secondaryFirstWhatsApp = true;
    secondarySecondWhatsApp = false;
    sibling = false;
    parentCountry = null;
    parentState = null;
    parentCity = null;
    statusId = null;
    subStatusId = null;
    programCatagoryId = null;
    programId = null;
    schoolId = null;
    sourceCatagory = null;
    primaryParent = null;
    secondaryParentType = null;
    parentKnowAboutUs = [];
    actionTaken = [];
    childGender = Gender.male;
    childPreSchool = YesNo.no;
    childDoB = null;
    addingNew = false;
  }

  resetForSibling() {
    childFirstName = null;
    childLastName = null;
    childGender = Gender.male;
    childDoB = null;
    sibling = false;
    notifyListeners();
  }

  Future addLead() async {
    Map<String, dynamic> data = {
      "child_first_name": childFirstName ?? '',
      "child_dob": childDoB == null ? DateTime.now() : childDoB!.toString(),
      "child_last_name": childLastName ?? '',
      "child_gender": childGender.name,
      "child_pre_school": childPreSchool.name,
      "programcategory_id": programCatagoryId,
      "program_id": programId,
      "school_id": schoolId,
      "primary_parent": primaryParent ?? 'Gaurdian',
      "parent_name": parentName ?? '',
      "parent_first_contact": parentFirstContact ?? '',
      "parent_second_contact": parentSecondContact ?? '',
      "parent_email": parentEmail ?? '',
      "parent_education": parentEducation ?? '',
      "parent_profession": parentProfession ?? '',
      "secondary_parent_name": secondaryParentName ?? '',
      "secondary_parent_type": secondaryParentType ?? '',
      "secondary_first_contact": secondaryFirstContact ?? '',
      "secondary_Second_contact": secondarySecondContact ?? '',
      "secondary_second_whatsapp": secondarySecondWhatsApp ? 1 : 0,
      "secondary_first_whatsapp": secondaryFirstWhatsApp ? 1 : 0,
      "secondary_whatsapp": secondaryFirstWhatsApp
          ? (secondaryFirstContact ?? '')
          : (secondarySecondContact ?? ''),
      "secondary_email": secondaryEmail ?? '',
      "secondary_education": secondaryEducation ?? '',
      "secondary_profession": secondaryProfession ?? '',
      "parent_landmark": parentLandmark ?? '',
      "parent_house": parentHouse ?? '',
      "parent_street": parentStreet ?? '',
      "parent_address": parentAddress ?? '',
      "parent_country": parentCountry ?? '',
      "parent_state": parentState ?? '',
      "parent_pincode": parentPinCode ?? '',
      "parent_area": parentArea ?? '',
      "parent_city": parentCity ?? '',
      "parent_know_aboutus": parentKnowAboutUs,
      "parent_whatsapp":
          whatsAppFirst ? parentFirstContact : parentSecondContact,
      "whatsapp_second": whatsAppSecond ? 1 : 0,
      "whatsapp_first": whatsAppFirst ? 1 : 0,
      "source_category": sourceCatagory ?? '',
      "status_id": statusId,
      "substatus_id": subStatusId,
      "remark": remark ?? '',
      "action_taken": actionTaken,
      "sibling": sibling ? 1 : 0
    };
    Map<String, dynamic> response = await addLeadRepository.addLeadApi(
      data: data,
    );

    if (response['code'] == 200) {
      log('response success ');
    } else {
      log('Error In Response');
    }
  }

  Future getPrograms({required String catId}) async {
    try {
      var response = await addLeadRepository.programApi(catId: catId);
      if (response['code'] == 200) {
        List<Programs> programList = List<Programs>.from(
          response["data"].map((e) => Programs.fromJson(e)),
        );

        // List<Programs> tempList =
        //     List<Programs>.from(response.map((e) => Programs.fromJson(e)));
        //notifyListeners();
        listPrograms = programList;
        //myTempList = tempList;
        notifyListeners();
        log('Success');
      }
    } catch (e) {
      log('Error in program response = ${e.toString()}');
    }
  }

  Future getCenters() async {
    try {
      var response = await addLeadRepository.centerApi();
      if (response['code'] == 200) {
        List<CenterModal> tempCenterList = List<CenterModal>.from(
            response["data"].map((e) => CenterModal.fromJson(e)));
        centerList = tempCenterList;
        notifyListeners();
        log('success');
      }
    } catch (e) {
      log('Error in getting center = ${e.toString()}');
    }
  }

  Future getCountries() async {
    try {
      var response = await addLeadRepository.countryApi();
      if (response['code'] == 200) {
        List<IndiaCountryModal> tempCountryList = List<IndiaCountryModal>.from(
            response["data"].map((e) => IndiaCountryModal.fromJson(e)));
        countryList = tempCountryList;
        notifyListeners();
        log('Success');
      }
    } catch (e) {
      log('Error in getting data from country provider = ${e.toString()}');
    }
  }

  Future getStates({required int countryId}) async {
    try {
      var response =
          await addLeadRepository.getStateByCountryId(countryId: countryId);
      if (response['code'] == 200) {
        List<StateByCountryId> tempStateList = List<StateByCountryId>.from(
          response["data"].map((e) => StateByCountryId.fromJson(e)),
        );
        stateList = tempStateList;
        notifyListeners();
      }
    } catch (e) {
      log('Error in getting data from state provider = ${e.toString()}');
    }
  }

  Future getCities({required int stateId}) async {
    try {
      var response = await addLeadRepository.getCityByState(stateId: stateId);
      if (response['code'] == 200) {
        List<CitiesByState> tempCity = List<CitiesByState>.from(
            response["data"].map((e) => CitiesByState.fromJson(e)));
        cityList = tempCity;
        notifyListeners();
      }
    } catch (e) {
      log('Error in cities proider = ${e.toString()}');
    }
  }

  Future getAllActionPlanned({required String statusId}) async {
    var response =
        await addLeadRepository.getAllActionPlanned(statusId: statusId);
    if (response['code'] == 200) {
      List<ActionPlannedModel> tempActionPlanned =
          List<ActionPlannedModel>.from(
        (response["data"].map((e) => ActionPlannedModel.fromJson(e))),
      );
      listOfActions = tempActionPlanned;
      notifyListeners();      
    }
  }
}
